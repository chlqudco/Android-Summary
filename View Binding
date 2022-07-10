- View Binding
	- 안드로이드 스튜디오는 뷰 바인딩이라는 형태로 앱 코드에서 레이아웃 뷰를 참조할 수 있다
	- 뷰 바인딩이 활성화 되면 app 모듈에 있는 각 레이아웃 파일의 바인딩 클래스를 자동으로 생성함
	- 네이밍 : 레이아웃파일 이름을 카멜 표기법으로 나타내고 제일 끝에 Binding을 붙임
		- ex) activity_main.xml -> ActivityMainBinding

- 활성화 하기
	- 모듈의 build.gradle 파일에서 아래 코드 추가
```
buildFeatures {
	viewBinding true
}
```
	- 그 다음 코틀린 파일에서 아래 작업 추가
```
private val binding by lazy {ActivityMainBinding.inflate(layoutInflater)}
setContentView(binding.root)
```
	- 그 뒤론 binding을 이용해 쉽게 접근할 수 있다
	- 함수 정의에서 with(binding)을 이용하면 binding을 생략해도 돼서 편하다
