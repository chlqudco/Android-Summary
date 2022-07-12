- DataBinding
	- ViewModel의 데이터를 XML 레이아웃 파일의 뷰와 직접 연결되게 해준다
	- 즉, 별도의 코드 작성 없이 ViewModel에 저장된 LiveData 값이 XMl 파일에서 직접 참조될 수 있다
- Data Binding
	- 주 목적은 UI 레이아웃의 뷰를 코틀린 코드에 저장된 데이터와 연결하는 간단한 방법을 제공하는 것
		- 코드라 함은 대게 ViewModel이다
	- 또한 다른 객체의 이벤트나 리스너 함수에 연결시키는 편리한 방법도 제공함
	- LiveData와 같이 사용될 때 특히 강력하다
	- 초기의 바인딩 설정 외에 추가로 작성할 코드가 필요 없다는 것이 장점이다
		- 여태까지는 버튼을 컨트롤러 함수에 연결할 때 필요한 코드를 직접 작성해야 했다

- 핵심 구성요소
	- 앱에서 데이터바인딩을 사용하려면 여러가지 요소가 결합되어야 한다
		- 빌드 구성, xml, 바인딩 클래스, 바인딩 표현식 언어
	- 프로젝트 빌드 구성
		- 데이터 바인딩을 사용하려면 활성화시키라는 뜻임. 어디서? build.gradel에서
		- viewBinding 대신 dataBinding 쓰면 끝남
	- xml 파일
		- 데이터 바인딩을 사용하려면 기존 XML 레이아웃 파일을 데이터 바인딩 레이아웃 파일로 바꿔야됨
		- 루트뷰(최상위 컨테이너)를 layout 컴포넌트로 바꿔야 함
		- 레이아웃 파일은 ViewModel이나 Activity등 과 바인딩 되어야 하며, 이 클래스의 이름이 레이아웃 파일에 선언되어야 함
		- 또한, 이 클래스의 인스턴스를 참조하는 변수 이름도 필요
		- 다른 클래스를 import할 수 있다
		- setVariable 함수를 통해 연결!
```
<layout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools">
    
    <data>
        <variable
            name="myViewModel"
            type="com.chlqudco.develop.arcticfox_book_viewmodel.ui.main.MainViewModel" />
    </data>
/>
```
	- 바인딩 클래스
		- data 요소에서 참조하는 각 클래스에 대응되는 바인딩 클래스는 자동으로 생성해준다
		- ViewBinding이랑 똑같다고 보면됨
		- 바인딩 클래스의 인스턴스를 생성하는 코드는 당연히 직접 작성해야 한다.
		- DataBindingUtil 클래스를 사용한다
```
        binding = DataBindingUtil.inflate(inflater, R.layout.fragment_main, container, false)
        binding.lifecycleOwner = this
        binding.setVariable(myViewModel, viewModel)
```

	- 바인딩 표현식(단방향)	
		- 특정 뷰가 바인딩 객체와 어떻게 상호작용하는지 정의
		- 선언 언어를 사용하여 여러가지 일을 할 수 있다.
		- 표준 자바 라이브러리가 import 되므로 많은 일을 수행할 수 있다
		- @로 시작하며 {}안에 표현식을 넣는다

```
android:text='@{safeUnbox(myViewModel.result) == 0.0 ? "Enter value" : String.valueOf(safeUnbox(myViewModel.result)) + "euros"}'
```

	- 바인딩 표현식(양방향)
		- 레이아웃 뷰의 값이 변경될 때 이것과 대응되는 데이터 모델 값이 변경되게 하자
		- @대신 @=쓰면 끝

```
android:text="@={myViewModel.dollarValue}"
```

	- 이벤트와 리스너 바인딩
		- 바인딩 표현식에서는 뷰의 이벤트에 대한 응답으로 함수를 호출할 수 있다
		- 리스너 바인딩으로는 인자를 전달하면서 함수를 호출할 수 있다
```
android:onClick="@{() -> myViewModel.convertValue()}"
```
