- 액티비티 생명주기
	- 앱이 실행되는 동안 액티비티도 서로 다른 상태로 전환한다
	- 액티비티 스택 안에서의 위치에 따라 결정된다

- 액티비티 스택
	- ART애서는 실행중인 각 앱에 대해 액티비티 스택을 유지, 관리 한다
	- 스택의 맨 위에 있는 액티비티를 활성화된 액티비티라고 한다
	- 구조가 그냥 stack 그 자체라 할 말이 없다.
	- 당연히 새로운 액티비티는 맨 위에 쌓인다

- 액티비티 상태(State)
	- 실행되는 동안 액티비티는 다음과 같은 상태를 갖는다
	- Active / Running
		- 스택의 맨 위에 있고, 화면에서 볼 수 있으며 사용자와 상호작용한다
		- 우선순위가 상당히 높다
	- Paused
		- 화면에서 볼 수 있지만 포커스를 갖고 있지 않은 경우
		- 다른 액티비티가 이 액티비티를 부분적으로 가리고 있기 때문
	- Stopped
		- 사용자가 볼 수 없는 액티비티
		- 아직까지 상대 정보를 보존 하고 있기는 함
	- Killed
		- ART가 종료시켜 버린 액티비티
		- 스택에도 남아있지 않음

- 구성 변경
	- 위의 내용 뿐만 아니라 장치 방향을 바꾸던지, 다크모드 키고 끄던지 등의 활동은 액티빅티를 재 생성한다
	- 리소스에 영향을 주는 변경이 생길때는 소멸 및 재생성하여 응답하는게 제일 빠른 방법이기 때문이다

- 상태 변경 처리
	- ART는 상태 변경을 앱에게 알려준다. 따라서 적절히 코드로 처리해야 함
	- 상태 변경이 생길 때는 내부 데이터 구조와 UI 상태 모두 저장 or 복원하는 작업이 필요함
	- 안드로이드는 두가지 방법을 제공한다
		- 운영체제가 호출해 주는 상태 변경 함수에서 응답하는 방법
		- Jetpack 생명주기 클래스를 사용하는 것
