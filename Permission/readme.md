- Runtime Permission
	- 위험 권한에 대해서는 사용자에게 직접 허가를 받아야 함
	- 버전 6 이전까지는 설치할 때 권한을 받아왔음
		- 지금도 이렇게 받는 애들이 있는데 보통 퍼미션이라고 부름
	- 카메라, 녹음, 위치, SMS 등등 

- 1. 매니페스트에 이용할 기능 퍼미션 쓰기

- 2. 권한이 필요한 작업은 실행 전 권한을 받았는지 확인해야 함
private fun setupPermission() {
        val permission = ContextCompat.checkSelfPermission(this, Manifest.permission.RECORD_AUDIO)
        
        if (permission != PackageManager.PERMISSION_GRANTED){
            //원하는 기능 실행
        }
    }

- 3. 권한 받아오기
private fun makeRequest() {
        ActivityCompat.requestPermissions(this, arrayOf(Manifest.permission.RECORD_AUDIO), RECORD_REQUEST_CODE)
    }

- 4. 권한 체크 하기
override fun onRequestPermissionsResult(requestCode: Int, permissions: Array<out String>, grantResults: IntArray) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults)
        
        when(requestCode){
            RECORD_REQUEST_CODE ->{
                if (grantResults.isEmpty() || grantResults[0] != PackageManager.PERMISSION_GRANTED){
                    //권한 얻기 실패
                } else{
                    //권한 얻기 성공
                }
            }
        }
    }

- 5. 퍼미션을 거절한 사람에게 이유를 보여줘야함
	- 이전에 퍼미션을 거절한적이 있으면 should 함수가 true를 반환함
if (permission != PackageManager.PERMISSION_GRANTED){
            //거절한 적이 있는 경우
            if(ActivityCompat.shouldShowRequestPermissionRationale(this, Manifest.permission.RECORD_AUDIO)){
                val builder = AlertDialog.Builder(this).apply {
                    setMessage("권한이 필요해요")
                    setTitle("권한 요쳥")
                    setPositiveButton("확인"){ dialog , id ->
                        makeRequest()
                    }
                }
                val dialog = builder.create()
                dialog.show()
            }
            else{
                //권한 받아오기
                makeRequest()
            }
        }
