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


- 최신과 종전의 생명주기 기법
	- 액티비티나 프래그먼트 내부에 생명주기 관련 함수를 구현한다
		- 생명 주기가 변경될 때 안드로이드 운영체제가 호출함
	- Jetpack 컴포넌트로 생명주기를 처리한다

- 생명주기 함수를 오버라이드하여 필요한 기능을 구현
	- 어떤 상황이던 onCreate() 는 반드시 구현해야 함

- 생명주기를 관리하는 목적은 적시에 액티비티 상태를 저장하거나 복원하는 것
	- 상태는 액티비티의 데이터와 UI데이터를 말함
	- 메모리 데이터 상태 정보는 지속적으로 유지되어야 하므로 영속적 상태(persistent state)라고 함
	- UI의 상태는 동적 상태(dynamic state)라고 함, 앱이 한번 실행되는 동안만 보존하면 됨
	- 두 상태의 차이를 이해하고 다른 저장방법을 써야 한다.
	- 영속적 상태를 저장하는 목적
		- 액티비티가 백그라운드에 있는 동안 종료되어 생기는 데이터 유실을 막음
	- 동적 상태를 저장하는 목적
		- UX를 증가시키기 위해

- 생명주기 함수
	- Activity나 Fragment는 생명주기 함수를 많이 갖고 있음
	- 상태가 변경될 때 이벤트 핸들러처럼 동작함

- onCreate()
	- 액티비티 인스턴스가 최초 생성될 때 호출, 초기화 하는데 이상적인 함수
	- 인자로는 동적 상태 정보를 포함할 수 있는 Bundle 객체가 전달됨

- onRestart()
	- 시스템에 의해 중단되었다가 다시 시작될 때 호출된다

- onStart()
	- 위의 두 함수가 호출된 후 곧바로 호출된다.
	- 액티비티가 스택의 맨위로 이동하면 이 함수 호출 뒤 onResume()이 호출된다.

- onResume()
	- 액티비티 스택의 맨 위에 있으며 사용자와 현재 상호작용하는 액티비티

- onPause()
	- 이 함수 호출 다음에는 onResume() 또는 onStop() 중 하나가 호출됨
	- 포그라운드로 돌아가는 경우 onResume(), 볼수 없게 되면 onStop() 호출
	- 이 함수 내부에서는 앱에서 아직 저장하지 않은 영속적 상태 데이터를 저장하는 작업을 하면 좋다
	- 시간이 오래 걸리는 작업은 피해야함

- onStop()
	- 액티비티가 사용자에게 더이상 보여지지 않을 때 호출된다
	- 이 함수 다음엔 onRestart나 onDestroy가 호출된다
	- 액티비티가 포그라운드로 가면 onRestart, 종료 되면 onDestroy가 호출된다

- onDestroy()
	- 액티비티가 곧 소멸될 때 호출된다
	- finish()함수를 호출한 경우, 메모리 부족이나 구성변경으로 인해 액티비티를 종료하는 경우
	- 하지만 액티비티가 종료될 때 항상 호출되는 것은 아님에 주의해야 함

- onConfigurationChanged()
	- 매니페스트에 configChanges 속성을 정의 하면 구성변경이 생길 때마다 이 함수가 호출된다.
	- 액티비티가 재시작 되지 않으며 Configuration 객체가 이 함수에 전달된다

---
- 아래 함수들은 Fragment 에만 적용되는 생명주기 함수이다

- onAttach()
	- 프래그먼트가 액티비티에 지정될 때 호출된다

- onCreateView()
	- UI 레이아웃 뷰 계층을 생성하고 반환하기 위해 호출된다

- onActivityCreated()
	- 연관된 액티비티의 onCreate()가 실행 완료되면 호출된다

- onViewStatusRestored()
	- 저장된 뷰 계층이 복원될 때 호출된다

---
- 액티비티의 동적 상태를 저장하고 복원하기 위해 만들어진 두개의 함수가 있다

- onRestoreInstanceState()
	- 상태정보가 저장되었던 이전 액티비티 인스턴스로부터 다시 생성되어 시작될 때 호출된다
	- onCreate와 마찬가지로  Bundle 객체가 인자로 전달된다
	
- onSaveInstanceState()
	- 동적 상태 데이터가 저장될 수 있도록 액티비티가 소멸되기 전에 호출된다
	- 동적 상태 데이터가 저장될 필요가 있다고 런타임이 판단한 경우에만 호출

- 생명주기 함수를 오버라이딩 할 때는 반드시 super 클래스 함수를 제일 먼저 호출해야 한다
	- 호출하지 않으면 익셉션이 발생된다

- 생애(LifeTime)
	- 전체 생애(Entire Lifetime)
		- onCreate와 onDestroy 사이를 전체 생애라고 부름
	- 가시적 생애(Visible Lifetime)
		- onStart와 onStop 사이의 시기를 나타낸다. 유저는 화면에서 액티비티를 볼 수 있다
	- 포그라운드 생애(Foreground Lifetime)
		- onResume과 onPause 사이의 시기를 나타낸다.
		- 액티비티나 프래그먼트는 전체 생애 동안 ㅍ그라운드와 가시적 생애를 여러번 거칠 수 있다
	
- 요즘은 폴더블 장치가 많아서 여러 앱의 액티비티가 동시에 resume 상태가 될 수 있다.
	- 결국 현재 사용자와 상호작용 하는 앱을 최상위 실행 재개 액티비티라고 한다

- 액티비티 재시작 방지
	- 앞서 언급한 것 처럼 매니페스트에 configChanges 속성값을 지정하면 재시작 되지 않도록 할 수 있다.
```
 <activity
            android:name=".MainActivity"
            android:configChanges="orientation|fontScale"
            android:exported="true">
        </activity>
```

- 생명주기 함수의 제약
	- 여러 해 동안 상태 변경을 처리하는데 유일한 메커니즘이었다.그러나 단점이 있다
	- 실행 중일 때 상태를 알아내는 쉬운 방법을 제공하지 않는다
		- 액티비티나 프래그먼트 자체에서 내부적으로 자신의 상태를 지속적으로 파악하거나 다음번 생명주기 함수가 호출될 때까지 기다려야 한다
	- 특정 객체가 다른 객체의 생명주기 상태를 관찰할 수 있는 방법을 제공하지 않는다
		- 앱의 많은 객체가 생명주기 상태 변경에 영향을 받을 수 있기 때문에 심각한 문제가 될 수 있다
	- Activity나 Framgent 클래스의 서브 클래스에서만 사용할 수 있다
		- 생명주기를 인식하는 커스텀 클래스를 만드는것이 불가능하다
	- 대부분의 생명주기 처리 코드를 내부에 작성해야 하므로 코드가 복잡해진다
		- 이상적으로는 다른 클래스에 있어야 한다
	- 이 모든 문제점은 생명주기-인식 컴포넌트를 사용하여 해결할 수 있다


- ![Android_activity_lifecycle_methods](https://user-images.githubusercontent.com/68932465/178191603-fb83a1c5-0db4-4e92-8ee3-21711d6ddda5.jpg)


- 대부분의 컴포넌트는 알아서 상태값을 저장하고 복원한다.
	- 그게 싫으면  android:saveEnabled="false" 속성을 주면 된다

- Bundle 클래스
	- 저장될 필요가 있는 동적 데이터를 onSaveinstanceState 함수에서 Bundle 객체에 저장해 두자
	- UI 컴포넌트의 자동 저장 메커니즘 이외에 저장 기능이 필요한 경우 저장하면 좋다
	- key-value 쌍으로 구성되는 데이터를 저장한다
	- 키는 문자열이며 value는 기본형 or Parcelable 인터페이스를 구현하는 어떤 객체도 가능하다

- 수동 저장 코드
```
    override fun onSaveInstanceState(outState: Bundle) {
        super.onSaveInstanceState(outState)
        Log.i(TAG, "onSaveInstanceState")
        
        val userText = binding.editText.text
        outState.putCharSequence("savedText", userText)
    }
```

- 수동 복원 코드
	- onCreate나 onRestoreInstanceState 둘 중 한곳에서 복원하면 된다.
	- 초기화 작업이 끝난 뒤에 복원하고 싶으면 후자를 선택
```
    override fun onRestoreInstanceState(savedInstanceState: Bundle) {
        super.onRestoreInstanceState(savedInstanceState)
        Log.i(TAG, "onRestoreInstanceState")
        
        val userText = savedInstanceState.getCharSequence("savedText")
        binding.editText.setText(userText)
    }
```

