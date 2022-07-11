- Gesture
	- 터치스크린과 사용자 간의 연속적인 상호작용을 정의하는데 사용된다
	- 전자책의 페이지 넘기기, 지도 줌인 줌아웃이 제스쳐 예시이다.
	- 안드로이드 SDK는 일반 제스처와 커스텀 제스처 모두 앱에서 감지하고 처리하기 위한 메커니즘을 제공한다
	- 일반제스처는 탭, 더블탭, 길게 누름, 플링 등이 있다
	- 일반 제스처를 감지하기 위해 GestureDetector 클래스를 사용한다

- 일반 제스처 감지와 처리
	- 사용자가 화면과 상호작용 할때는 MotionEvent로 확인한다
	- 모션이 일반 제스처와 일치하는지 쉽게 확인할 수 있다.
	
- 감지 순서
	- OnGestureListener 인터페이스를 구현하는 클래스를 정의한다.
		- 새로운 클래스이거나 액티비티 클래스일 수 있다.
		- 원하는 콜백 함수를 구현한다
```
class MainActivity : AppCompatActivity(), GestureDetector.OnGestureListener, GestureDetector.OnDoubleTapListener {

    override fun onDown(p0: MotionEvent?): Boolean {
    }

    override fun onShowPress(p0: MotionEvent?) {
    }

    override fun onSingleTapUp(p0: MotionEvent?): Boolean {
    }

    override fun onScroll(p0: MotionEvent?, p1: MotionEvent?, p2: Float, p3: Float): Boolean {
    }

    override fun onLongPress(p0: MotionEvent?) {
    }

    override fun onFling(p0: MotionEvent?, p1: MotionEvent?, p2: Float, p3: Float): Boolean {
    }

    override fun onSingleTapConfirmed(p0: MotionEvent?): Boolean {
    }

    override fun onDoubleTap(p0: MotionEvent?): Boolean {
    }

    override fun onDoubleTapEvent(p0: MotionEvent?): Boolean {
    }
}
```
	- 앞에서 만든 클래스의 인스턴스를 인자로 전달하면서 제스쳐디텍터컴팻 인스턴스를 생성한다
```
var gDetector: GestureDetectorCompat? = null
this.gDetector = GestureDetectorCompat(this,this)
gDetector?.setOnDoubleTapListener(this)
```

	- 액티비티에 onTouchEvent를 구현한 뒤 MotionEvent를 인자로 전달하여 비교한다.
```
override fun onTouchEvent(event: MotionEvent?): Boolean {
        this.gDetector?.onTouchEvent(event)
        return super.onTouchEvent(event)
    }
```
