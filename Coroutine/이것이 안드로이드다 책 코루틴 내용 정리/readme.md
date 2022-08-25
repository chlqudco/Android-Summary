- 코루틴 소개
	- 코루틴에서 쓰레드는 단지 코루틴이 실행되는 공간을 제공하는 역할만 함
	- 쓰레드를 중단시키지 않기 때문에 하나의 쓰레드에 여러 개의 코루틴이 존재 가능
	- 쓰레드 간의 전환을 컨텍스트 스위칭이라 하는데 이걸 안해서 이득임

- 코루틴 스코프
	- 코루틴은 정해진 스코프 안에서 실행됨
	- 코루틴 코드들은 정해진 스코프 안에서 동작해야 함
	- GlobalScope와 CoroutineScope가 있음, 글로벌 안쓸거임.
		- 서버 통신이나 파일여는, 걍 계속 CoroutineScope 쓰셈 일단.
	- CoroutineScope(Dispatchers.IO).launch {  }

- 디스패처
	- 위 코드의 Dispatchers.IO를 디스패처라고 함
	- 코루틴이 실행될 쓰레드를 지정하는 장치
	- IO, Main, Default, Unconfined 등이 있는데 걍 IO 랑 Main만 알면 됨
	- Main은 UI 작업이 필요한 경우 쓰고
	- 나머지는 걍 IO로 쓰셈 일단

- 코루틴 시작
	- 코루틴은 launch나 async로 시작할 수 있다.
	- 둘다 job을 반환 하는데 이걸로 코루틴을 조절할 수 있다.
	
- 코루틴 컨트롤
	- cancel
		- 코루틴 멈추기
		- 하위 코루틴도 모두 멈춤
	- join
		- 코루틴 스코프 안에 선언된 여러 launch 블록은 모두 새로운 코루틴으로 분기되면서 동시에 처리됨
		- 따라서 순서를 정할 수 없는데 순서를 정하기 위해 launch 뒤에 join()을 쓰면 각 코루틴이 순차적으로 실행됨

```
CoroutineScope(Dispatchers.IO).launch { 
            launch { 
                for (i in 0..5){
                    delay(500L)
                    Log.d("코루틴", "결과1 = $i")
                }
            }.join()
            
            launch {
                for (i in 0..5){
                    delay(500L)
                    Log.d("코루틴", "결과2 = $i")
                }
            }
        }
```

- async
	- async는 코루틴 스코프의 연산 결과를 받아서 사용할 수 있음
	- 시간이 오래 걸리는 코루틴을 async로 시작하고, 결과값을 사용하는 곳에서 await()를 사용하면 결과 처리가 완료된 뒤에 await()를 호출한 줄의 코드가 실행됨

```
        CoroutineScope(Dispatchers.IO).async { 
            val deferred1 = async { 
                delay(500L)
                350
            }
            val deferred2 = async { 
                delay(1000L)
                200
            }
            Log.d("코루틴", "연산 결과 = ${deferred1.await() + deferred2.await()}")
        }
```

- suspend
	- 코루틴 안에서 suspend 키워드로 선언된 함수가 호출되면 이전까지의 코드 실행이 멈추고 suspend 함수의 처리가 완료된 뒤에 멈춰 있던 원래 스코프의 다음 코드가 실행됨
	

```
    suspend fun subRoutine(){
        for (i in 0..10){
            Log.d("코루틴", "$i")
        }
    }

        CoroutineScope(Dispatchers.IO).launch {
            // 코드 블럭 1
            subRoutine()
            // 코드 블럭 2
        }

```

- 코드 블럭 1을 끝내고 서브루틴 함수가 다 끝난 뒤에 코드블럭 2를 실행함.
	- PS 하는것 처럼 순차적 구조라고 보면 편함

- withContext
	- suspend 함수를 호출할 때 호출한 스코프와는 다른 디스패처(다른 쓰레드)에서 돌리고 싶은 경우가 있다.
	- 그럴 때 withContext를 사용해서 디스패처를 변경할 수 있다.

```
        CoroutineScope(Dispatchers.IO).launch {
            // 코드 블럭 1
            val result = withContext(Dispatchers.Main){
                // 메인 쓰레드 처리
                // 당연히 suspend 함수로 반환값을 받아올 수 있다.
            }
            // 코드블럭 2
        }
```

- 이미지 불러오는 코드 예시

```
        binding.button.setOnClickListener {
            CoroutineScope(Dispatchers.Main).launch { 
                //프로그래스바 보이기
                val url = editText.text.toString()
                val bitmap = withContext(Dispatchers.IO){
                    //이미지 불러오는 함수, 당연히 suspend로 작성해야 됨
                }
                imageView.setImageBitmap(bitmap)
                //프로그래스바 숨기기
            }
        }
```
