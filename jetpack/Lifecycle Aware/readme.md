
- LifeCycle Aware 컴포넌트
	- 여태까지는 컨트롤러에서 생명주기 함수를 사용해서 변화를 처리했다
		- 이 방법은 생명주기 변화 처리 부담을 컨트롤러에게 가져다준다
	- 상태변화로 영향을 받는 코드는 다른 클래스에 있다
		- 따라서 컨트롤러에 구현하면 코드가 비대해 진다
	- 해결법 : 한 객체가 다른 객체의 생명주기 상태를 관찰하고 대응할 책임을 갖도록 하자
		- 아키텍쳐 컴포넌트에 포함된 생명주기 패키지의 클래스와 인터페이스를 사용
	
- 생명주기 인식
	- 앱에 있는 다른 객체의 생명주기 상태 변화를 관찰하고 응답할 수 있는 객체
		- LiveData는 이미 생명주기 인식을 한다 -> 먼소리?
	- LifecycleObserver 인터페이스만 구현하면 어떤 클래스도 생명주기 인식을 하도록 구성할 수 있다

- 생명주기 인식 소유자
	- 생명주기 인식 컴포넌트는 생명주기 소유자 객체의 상태만 관찰 가능하다
	- 소유자는 LifecycleOwner 인터페이스를 구현, 짝을 이루는 Lifecycle 객체에 지정
	- 생명주기 옵저버에게 상태 정보를 제공하는 책임을 갖는다
	- 액티비티나 프래그먼트등 대부분은 생명주기 소유자이다 

- 생명주기 옵저버
	- 생명주기 소유자의 상태를 관찰하려면 LifecycleObserver 인터페이스를 구현해야 한다
	- 또한, 관찰할 필요가 있는 생명주기 상태를 처리하는 이벤트 리스너 핸들러를 작성해야 함
	- 더이상 관찰할 필요가 없다면 언제든 제거할 수 있다

- 생명주기 상태
	- 생명주기 소유자는 5개중 하나의 상태를 갖는다
	- INITIALIZED, CREATED, STARTED, RESUMED, DESTROYED
	- 옵저버는 어노테이션을 사용해서 함수와 생명주기 이벤트를 연관시킨다
	- ON_ANY로 지정하면 모든 생명주기 이벤트에 대해 호출된다


- 구현
1. 생명주기를 관찰할 수 있는 클래스 추가

```
class DemoObserver: LifecycleObserver {
    
    @OnLifecycleEvent(Lifecycle.Event.ON_RESUME)
    fun onResume(){
    }
}
```

2. 메인액티비티? 그.. 관찰당하는 객체에 옵저버 추가하기

```
lifecycle.addObserver(DemoObserver())
```

- 커스텀 생명주기 소유자 클래스 생성
	- 이벤트를 발생시키고 생명주기 상태를 변경할 수 있다
	- 자신의 인스턴스 참조로 초기화된 레지스트리 인스턴스가 필요
	- markState나 handleLifecycleEvent 함수로 생명주기 이벤트를 발생시킨다

```
class DemoOwner: LifecycleOwner {
    
    private val lifecycleRegistry: LifecycleRegistry
    
    init {
        lifecycleRegistry = LifecycleRegistry(this)
    }
    
    override fun getLifecycle(): Lifecycle {
        return lifecycleRegistry
    }

    fun startOwner(){
        lifecycleRegistry.handleLifecycleEvent(Lifecycle.Event.ON_START)
    }
    
    fun stopOwner(){
        lifecycleRegistry.handleLifecycleEvent(Lifecycle.Event.ON_STOP)
    }
}
```
