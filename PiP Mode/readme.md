- PiP 모드
	- PictureInPicture
	- 화면 크기를 작게 해서 동영상 재생하기
	- 이 상태에 있는 액티비티는 다른 액티비티와 무관하게 계속 실행됨

- API 26 이상에서만 지원됨
	- 매니페스트에서 모드 활성화 하기
	- configChaneges 속성을 주지 않으면 액티비티가 다시 시작되므로 동영상이 맨 처음으로 감
	- PIP객체 생성후 속성 설정하기

- 매니페스트 활성화
           - android:supportsPictureInPicture="true"
           - android:configChanges="screenSize|smallestScreenSize|screenLayout|orientation"

- pip 시작
	- enterPictureInPictureMode(params)

- 모드 변경 감지
	- override fun onPictureInPictureModeChanged()
	- isInPictureInPictureMode 사용하면 됨
