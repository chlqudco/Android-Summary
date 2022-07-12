- 내비게이션 아키텍처 컴포넌트
	- Jetpack이 등장하기 이전에는 매우 복잡한 화면 이동 경로를 구성하는 쉬운 방법이 없었다. 많은 코드를 작성해야 했음
	- 화면 이동을 쉽게 해주는 아이
	- 앱을 구성하는 각 화면을 목적지라고 하며 대게 액티비티나 프래그먼트가 된다
	- 네비게이션 스택을 사용해서 내부 목적지 경로를 추적함
	- 목적지 이동과 스택 관리의 모든 작업은 내비게이션 컨트롤러가 처리

- 내비게이션 호스트
	- 내비게이션 호스트는 특별한 프래그먼트 이다
	- 액티비티 UI에 포함되어 사용자가 이동하는 목적지의 placeHolder로 사용된다
	- 영역이다
	- 파레트에서 NavHostFragment 끌어오면 됨
	- name 속성은 노건들, defaultNavHost는 true로 설정
	- navGraph 속성에는 내비게이션 그래프 파일을 지정
	- 액티비티가 시작될 때 홈 목적지가 들어간다

```
    <androidx.fragment.app.FragmentContainerView
        android:id="@+id/demo_nav_host_fragment"
        android:name="androidx.navigation.fragment.NavHostFragment"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:defaultNavHost="true"
        app:navGraph="@navigation/navigation_graph" />
```

- 내비게이션 그래프
	- 앱 화면 이동에 포함되는 목적지를 갖는 XML파일
	- 목적지 외에도 내비게이션 액션을 포함한다
		- 목적지 간의 이동과 데이터를 전달하기 위한 인자를 정의
	- 작업하는 그 화면 말하는거 맞음

- 내비게이션 컨트롤러
	- 내비게이션 액션이 실행되려면 코드에서 컨트롤러 참조를 얻어야 함
	- findNavController 함수로 찾아
	
- 내비게이션 액션
	- 화면 이동을 해야지!
	- 컨트롤러의 navigate 함수를 쓰면 됨.

- 인자 전달
	- 목적지로 데이터를 전달할 수도 있음
	- argument 태그로 지정하면 됨
	- 전달에는 두가지 방법이 있다
	- 번들 객체에 인자를 넣는 방법
		- 타입에 안전하지 않아서 런타임 에러 가능성이 있다
	- safeargs를 사용하는 법
		- 안스의 그래들 빌드 시스템의 플러그인이다
		- 타입에 안전한 방법으로 인자가 전달될 수 있게 해주는 클래스를 자동 생성한다
	
- 구현

1. 의존성 추가

```
    implementation 'androidx.navigation:navigation-fragment-ktx:2.4.2'
    implementation 'androidx.navigation:navigation-ui-ktx:2.4.2'
```

2. 내비 그래프 생성하기
	- res 폴더 우클릭 후 New -> Android Resource File 선택후 그래프 만들기

3. 내비 호스트 선언하기
	- 원하는 액티비티에서 팔레트에서 NavHost 끌어오기

4. 그래프에서 원하는 목적지 추가하기

5. 내비게이션 그래프에 액션 추가하기
	- 걍 점 두개 이으면 됨

```
        <action
            android:id="@+id/mainToSecond"
            app:destination="@id/secondFragment" />
```

6. 프래그먼트와 액티비티간 통신을 위한 리스너 구현

```
    interface OnFragmentInteractionListener{
        fun onFragmentInteraction(uri: Uri)
    }
```

7. 액션 구현하기

```
        binding.button.setOnClickListener { 
            Navigation.findNavController(it).navigate(R.id.mainToSecond)
        }
```

8. 인자 전달 할 거면 safeargs를 쓰자
	- 그래들에 플러그인 추가
	- 여기가 맞는지 모르겠삼

```
프로젝트 수준
buildscript {
    dependencies {
        classpath 'androidx.navigation:navigation-safe-args-gradle-plugin:2.4.2'
    }
}

앱 수준
id 'androidx.navigation.safeargs'
```

	- 목적지에서 받을 인자를 정의

```
        <argument
            android:name="message"
            app:argType="string"
            android:defaultValue="No Message" />
```

	- 출발지에서 전달하기

```
            var action: MainFragmentDirections.MainToSecond = MainFragmentDirections.mainToSecond()
            action.setMessage(binding.userText.text.toString())
            Navigation.findNavController(it).navigate(action)
```

	- 도착지에서 값 받기

```
override fun onStart() {
        super.onStart()
        arguments?.let { 
            val args = SecondFragmentArgs.fromBundle(it)
            binding.argText.text = args.message
        }
    }
```

