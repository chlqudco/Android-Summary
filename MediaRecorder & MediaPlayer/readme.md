- 녹음 및 재생

- 오디오 재생은 MediaPlayer 또는 AudioTrack 클래스를 이용할 수 있다.
	- AudioTrack은 스트리밍 오디오 버퍼를 쓰며, 더 풍부한 오디오 제어를 제공
	- MediaPlayer는 재생을 구현하기 쉬운 인터페이스를 제공

- MediaPlayer 클래스는 다양한 함수를 갖고 있다
	- create, setDataSource, prepare, start 등등
	- 구현방법 : 인스턴스를 생성하고 오디오 소스를 설정한뒤 prepare, start순서로 호출하면 끝

- MediaRecorder
	- 녹음 방법은 여러가지 있고 그중 하나임
	- 당연히 많은 함수 제공
	- 구현 방법 : 인스턴스 생성 뒤 여러 설정을 한 뒤 prepare, start 호출
	- 녹음 권한 받아와야 함

- 장치의 마이크가 있는지도 확인 해줘야 함
	- 쉬운 방법 : 특정 기능의 패키지가 설치되어 있는지 안드로이드에 확인을 요청
```
    private fun hasMicrophone(): Boolean{
        return packageManager.hasSystemFeature(PackageManager.FEATURE_MICROPHONE)
    }
```


- 녹음하기
```
fun recordAudio(view: View) {
        isRecording = true
        binding.stopButton.isEnabled = true
        binding.playButton.isEnabled = false
        binding.recordButton.isEnabled = false

        //초기 설정
        try {
            mediaRecorder = MediaRecorder().apply {
                setAudioSource(MediaRecorder.AudioSource.MIC)
                setOutputFormat(MediaRecorder.OutputFormat.THREE_GPP)
                setOutputFile(audioFilePath)
                setAudioEncoder(MediaRecorder.AudioEncoder.AMR_NB)
                prepare()
            }
        } catch (e: Exception){
            e.printStackTrace()
        }

        mediaRecorder?.start()
    }
```
- 녹음 중지
```
fun stopAudio(view: View) {
        binding.stopButton.isEnabled = false
        binding.playButton.isEnabled = true
        
        //녹음중이였다면
        if (isRecording){
            binding.recordButton.isEnabled = false
            mediaRecorder?.stop()
            mediaRecorder?.release()
            mediaRecorder = null
            isRecording = false
        } else{
            mediaPlayer?.release()
            mediaPlayer = null
            binding.recordButton.isEnabled = true
        }
    }
```

- 녹음 재생
```
fun playAudio(view: View) {
        binding.playButton.isEnabled = true
        binding.recordButton.isEnabled = true
        binding.stopButton.isEnabled = true
        
        mediaPlayer = MediaPlayer().apply { 
            setDataSource(audioFilePath)
            prepare()
            start()
        }
    }
```
