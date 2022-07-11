- 이벤트
	- 이벤트는 다양한 형태로 생길 수 있다
	- 대부분은 사용자 액션에 대한 응답으로 발생한다
	- 터치스크린과의 상호작용을 입력 이벤트 라고 한다
	- 안드로이드는 발생된 이벤트를 이벤트 큐에서 유지 관리 한다
	- 이벤트를 처리하기 위해서는 뷰에서 이벤트 리스너를 갖고 있어야 한다
		- 리스너는 콜백 추상 함수를 포함한다

- XML 파일의 뷰에서 onClick 속성 지정하기
	- android:onClick ="함수이름" 을 통해 이벤트를 지정할 수 있다
	- 이벤트 핸들러 처럼 다양한 옵션을 제공 하지 못한다
	- 프래그먼트와 관련된 레이아웃에서는 사용상 제약이 있다

---

- 이벤트 리스너 종류
	
- onClickListener
	- 뷰가 점유하는 장치 화면의 영역을 사용자가 터치한 다음 바로 떼었을 때 발생하는 클릭 형태의 이벤트 감지
	- onClick() 함수와 대응된다

- onLongClickListener
	- 뷰를 길게 터치한 것을 감지하는데 사용된다.
	- onLongClick() 함수와 대응된다

- onTouchListener
	- 터치스크린과의 모든 접촉을 감지하는데 사용된다
	- onTouch() 함수와 대응된다

- onCreateContextMenuListener
	- 길게 클릭했을 때 나타나는 컨텍스트 메뉴의 생성을 감지한다.
	- onCreateContextMenu() 함수와 대응된다

- onFocusChangeListener
	- 트랙볼이나 내비게이션 키를 누름으로써 현재 뷰에서 포커스가 빠져나가는 것을 감지
	- onFocusChange() 함수와 대응된다

- OnKeyListener
	- 뷰가 포커스를 갖고 있을 때 장치의 키가 눌러진 것을 감지하는데 사용된다
	- onKey() 함수와 대응된다

```

        binding.myButton.setOnClickListener { 
            binding.statusText.text = "Button Clicked"
        }
        
        binding.myButton.setOnClickListener(object : View.OnClickListener{
            override fun onClick(p0: View?) {
                
            }
        })
        
```	

- 어떤 리스너는 이벤트를 소비했는지 여부를 ART에 알려주어야 한다.
	- true를 반환하면 처리가 끝난 것으로 간주하여 해당 이벤트는 폐기한다
	- false를 반환하면 해당 이벤트를 동일한 뷰에 등록한 그 다음의 일치하는 이벤트 리스너에 전달한다
```
binding.myButton.setOnLongClickListener { 
            binding.statusText.text = "Long Clicked"
            true
        }
```

- 터치 이벤트
	- 대부분의 안드로이드 장치는 한 번에 하나 이상의 터치를 감지할 수 있다
	- 한 지점으로 제한되지 않고, 미끄러지듯 움직이는 터치도 감지할 수 있다
	- 터치는 또한 제스처로 해석될 수 도 있다
		- ex) 수평으로 미는 동장은 페이지를 넘기는 것으로 여겨진다
		- ex) 지도를 두손가락으로 늘리거나 줄이는 행위
	- 클릭은 컴포넌트, 터치는 뷰다

- 터치 이벤트 처리하기
	- 인자로는 이벤트가 발생한 뷰와 MotionEvent 타입 객체가 전달된다
		- MotionEvent 객체는 이벤트의 정보를 얻는 열쇠다.
		- 뷰안의 터치 위치와 수행된 액션 탕비이 들어 있다.

```
        binding.myLayout.setOnTouchListener { view, motionEvent -> 
            //필요한 작업
            true
        }
```

- 터치 액션 이해하기
	- MotionEvent 객체의 getActionMasked() 함수로 액션 타입을 얻을 수 있다.
	- 터치 시작은 ACTION_DOWN, 터치 중 움직임은 ACTION_MOVE, 터치 끝은 ACTION_UP
	- 하나 이상의 터치가 동시에 발생할 때 포인터 라고 한다
		
- 다중 터치 처리하기
	- 포인터는 인덱스값과 지정된 id로 참조한다
	- 해당 시점의 포인터 개수는 getPointerCount()로 참조한다
