
- in : 인치
- mm : 밀리미터
- pt : 포인트(1/72인치)
- dp : 밀도 독립적 픽셀, 장치 화면의 1/160인치를 나타냄, 화면 밀도와 무관하게 일정한 크기를 갖음
- sp : 크기 독립적 픽셀, 사용자가 선택한 폰트 크기를 고려한 dp이다
- px : 물리적인 화면 픽셀. 장치마다 레이아웃이 다르게 나타날 수 있음

- 안스 프로그램 램 사용량 설정을 조절할 수 있다, 너무 렉걸리면 설정하기(폰 램 얘기 아님;)
	- File -> Settings -> System Settings -> Memory Settings 에서 힙사이즈 늘리기

- 모든 단축키 보기
	- Help -> Keymap Reference

- 매개변수 정보 보기
	- 컨트롤 P

- 코드 한꺼번에 접거나 펴기
	- 컨트롤 쉬프트 +or-

- API 문서? 보기
	- 컨트롤 큐

- 코드 스타일 변경
	- File -> Settings -> Editor -> Code Style

--- 
- 기본 내용 정리
- 
- Bundle 클래스
	- 동적 상태 데이터를 저장하고 복원
	- onSaveInstanceState() 함수 호출 때 정보를 저장할 수 있는 기회를 가짐
	- 저장 해두면 onCreate나 onRestoreInstanceState 호출 할때 인자로 전달됨
	- 대부분의 뷰 위젯은 알아서 저장하고 불러옴, 개 혜자임, xml에서 saveEnabled로 조절 가능
	- 데이터 저장
		- 번들 변수?.put자료형Sequence(키,밸류)
	- 데이터 복원
		- 번들 변수.get자료형Sequence(키)


----------------------------------------------kt----------------------------------------------


-레이아웃 인플레이터
	-레이아웃에 뷰를 추가해줌, 리니어랑 쓰면 좋음
	-val 변수 = 레이아우 인플래이터.from(this).inflate(R.레이아웃,널,false)
	-위 작업으로 인해 붙일수 있는 뷰? 하나가 생성됨
	-레이아웃.addView(변수) 로 넣어주면 됨


-레이아웃 모든 뷰 삭제
	-레이아웃.removeAllViews()


- 쓰레드
	- 쓰레드 만드는 법
		- 쓰레드 객체 생성
			- Thread()를 상속받는 클래스를 정의하고 run을 오버라이드
			- run에서 하고싶은 일 적고 객체 생성해서 start() 하면 쓰레드 시작
		- 러너블 인터페이스를 상속
			- 쓰레드는 클래스라 다중상속이 안ㅇ되니까 러너블을 상속받아서 아까랑 똑같이 구현
			- 하지만 객체 생성할때는 Thread()로 묶어서 만들어야함.
		- 람다식으로 구현
			- 메인에서 바로 Thread{ 할일  }.start
	- 잠시 쉬었다 가는법
		- 람다 안이던 run안이던 Thread.sleep(초) 넣기

	- 핸들러와 루퍼 : 576쪽
	- 쓰레드 만들기
		- 변수 = Thread(Runnable{  }).start()
		- 메인쓰레드가 아니면 UI에 접근 불가
	- 메인쓰레드 접근
		- runOnUiThread{ }
		- 핸들러변수.post{ 랑 똑같 }
	- 변수 = Runnable{ 할일 }




- 핸들러
	- 메인쓰레드와 연결해주는 친구?
	- 변수 = Handler(Looper.getMainLooper())  (메인루퍼를 넣어서 메인쓰레드에 연결됨)
	- 변수.removeCallbacks(러너블 변수) , 실행되지 않고 팬딩되어있는 러너블을 지워줌
	- 변수.postDelayed(러너블 변수,초), 초 마다 러너블 객체가 실행됨
	- 루퍼는 앱이 실행되면 자동으로 생성되어 무한루프, 핸들러는 직접 생성해야됨


- 메세지
	- 루퍼의 큐에 값을 전달하기 위해 쓰는 클래스


- 코루틴
	- 스레드를 경량화한 도구


- 셰어드 프리퍼런스
	- ?? 의존성 추가해야됨?? 아 프리퍼런스 스크린.. 옵션창 만들꺼면 489쪽
		- "androidx.preference:preference-kts:1.1.1"
	- 파일에 저장하는 방식
	- 내부 저장소 사용, 권한처리 필요 X
	- 주로 로그인 정보나 앱의 상태정보 저장
	- 셰어드프리퍼런스 불러오는법
		- val 변수 = getSharedPreferences(이름,모드(Context,MODE_PRIVATE만 쳐 쓰셈))
		- 액티비티 하나밖에 없으면 이름 생략 가능
	- 값 가져오는법
		- 변수.get자료형(키,디폴트값)
	- 값 저장하는법
		- 변수.edit{ putString(키,밸류) commit() or apply() }
		- 변수.edit(true){}로 하면 커밋 안써도 됨
	- 커밋 : 저장 될때까지 UI멈춤,
	- 어플라이 : 비동기적으로 쓰레드로 돌림



- 프래그먼트
	- onCreateView 인자 3개 이는거 빼고 다 지우기
	- 알아서 xml만들고 메인에 프레임레이아우 만들고
	- val 변수 = supportFragmentManager.beginTransaction()
	- 프래그먼트 씌우기
		- 변수.add(R.id.프레임레이아웃, 프렉먼트())
		- replace로 교체하기
	- 변수.commit()
	- 변수.addToBackStack() 추가하면 뒤로가기로 맨위 프래그먼트 삭제	
	- 아니면 메인레이아웃에서 프레그먼트컨테이너뷰로 추가

	- 값 전달하기 : 번들 사용 378쪽


- 카운트다운 타이머
	- CountDownTimer(몇초동안, 몇초 간격으로){
		- 온틱(남은시간) : 매 간격마다 뭘할꺼냐
		- 온피시니 : 끝나면 머할거냐
	}.start()


- 애니메이션 효과
	- 뭐 어떤 뷰.animate()
		.alpha() : 투명도
		.setDuration() : 지속되는 시간
		.start() : 시작


----------------------------------------------나머지------------------------------------------------------


- 셰이프 드로어블 
	- xml로 도형(길) 만들기(드로어블 객체 생성)
	- 이미지 파일보다 용량도 작고 수정도 쉬움
	- 최상위 태그 : shape, rectangle
		- 원 : oval
	-최상위 태그 : ripple = 눌렀을 때 클릭하는거 같은 효과, 컬러값 지정
		- 그 안에 아이템 태그 넣고 쉐이프를 만듬
	- 배경 : solid태그, color=
	- 크기 : size 태그, width,height
	- 코너 : 둥그런 효과 radius
	- stroke : 테두리값, width와 컬러값
	- xml에 넣는법
		- background 태그로 넣기
	- 코드에서 넣는법
		- 변수.background = ContentCompat.getDrawable(컨텍스트,R.drawble.이름)

- 컨텍스트
	- 시스템을 사용하기 위한 프로퍼티와 매서드가 들어있는 클래스
	- 액티비티는 컨텍스트를 상속받는중
	- 종류
		- applicationContext
		- basecontext, 다른말로 this
	

- 스피너 : 여러 목록 중 하나 선택
	- 너무 간단하니 구현은 330쪽


- kapt란?
	-커틀린에서 어노테이션 쓸수 있도록 하기 위한 것

- 화면 가로로 보기
	- 메니페스트의 액티비티 속성에 스크린오리엔테이션을 랜드스케이프로 주기


- 시크바 쓰는법
	- 1. xml에서 시크바를 알아서 쳐 넣기
	- 2. xml에서 max 값을 지정해주기
	- 3. kt에서 시크바 불러오기
	- 4. 시크바에 셋온시크바 체인지 리스터 (object: 시크바.온시크바체인지 리스너 { 오버라이드 3개 }) 하기
	- 5. 온프로그레스체인지드 함수에서 값을 가져오면 됨.
		- 프롬 유저인지 코드에서 바뀐건지 잘 확인해야함
	- 온스탑트래킹 터치는 프로그래스바에서 손뗀순간에 뭘 할건지
	- 온스타트트래킹터치는 프로그래스바에서 손댄 순간에 뭘 할건지
	- 시크바 위치 조절 : 시크바.progress = 값
	- 시크바 꾸미기
		- 손잡이 바꾸기
			- thumb = "벡터 이미지"
		- 눈금 바꾸기
			- 색깔 바꾸기 : 프로그래스 드로어블 = " 컬러주기"
			- 눈금 표시하기 : app:tickMark = "드로어블이미지"
				- 쉐이프 드로어블 하나 만들기

- 사운드풀
	- 오디오,비디오? 파일을 도와주는 클래스
	- 변수1 = SoundPool.Builder().build() (사운드풀 총괄)
	- 변수2(인트형) = 변수1.load(this, R.폴더.이름 , 1)
	- 변수1.play(변수2, 1F, 1F, 0, 반복할래?(할꺼면 -1, 아니면 0), 1F)
	- 앱꺼도 재생하니까 생명주기 잘 관리해야됨(온포즈 때 변수1.autoPause(), 온리쥼 때 변수1.autoResume())
	- 온디스크로이 일때 변수1.realease() 해주기



- 앱 첫 시작의 화면부터 바꾸기
	- 테마에서 item name = "윈도우백그라운드">로 색갈지정
	
- 맨위 스테이터스바 색갈 바꾸기
	- 테마에서 스테이터브바 컬러 뒤 tools는 버리고 색깔 지정해주기


- 코틀린으로 커스텀으로 컴포넌트 만들기
	- 코틀린 클래스에서 해당 컴포넌트를 상속받고 인자는 앵간하면 2개 ex)
		class CustomButton(context: Context, attrs: AttributeSet): AppCompatImageButton(context, attrs){}


-FCM
	-앱?에 알림 보내는 기능
	-알림메세지와 데이터메세지로 나뉨
	-대부분 데이터메세지를 사용
	-알림메세지는 구현이 쉽지만 여러 케이스에서 대응이 힘듬
	-데이터 메세지는 앱에서 자체적으로 처리?


	-의존성에 implementation 'com.google.firebase:firebase-messaging-ktx' 추가

	-알림 메세지는 간단하게 테스트로도 보낼 수 있음

	-아래론 다 데이터 메세지
	
	-FirebaseMessagingService()를 상속받은 클래스 하나 만들기
		- onNewToken 오버라이드
			-토큰은 자주 갱신되는데 그걸 직접 처리하기엔 무리가 있으니 서버에 자동 갱신
		- onMessageReceived()도 오버라이드
			-메세지를 수신할때마다 얘가 호출됨
		- 노티피케이션 잘 만들기...

	-메니페스트에 <service android:name=".MyFirebaseMessagingService"
            			android:exported="false">
            			<intent-filter>
                			<action android:name="com.google.firebase.MESSAGING_EVENT"/>
            			</intent-filter>
        		</service> 추가

	-https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages/send?apix=true 에서 잘 작성한 다음


-Notification
	-알림 이나 뭐든 상태바 내리면 나오는거?
	-자주 기능이 업뎃 되니까 호환성 잘 체크
	-채널을 만들어야 됨
	-채널은 앱을 시작할때 만드는게 안전
	-중요도 설정하기
		-중요도에 따라 발생하는일? 이 다름

	-코드 작성
private fun createNotificationChannel(){
	-오레오 이상은 채널을 만들어야 하니까 ㅎㅎ;
        if(Build.VERSION.SDK_INT >= Build.VERSION_CODES.O){
            val channel = NotificationChannel(CHANNEL_ID, CHANNEL_NAME,NotificationManager.IMPORTANCE_HIGH)
            channel.description = CHANNEL_DESCRIPTION
            (getSystemService(Context.NOTIFICATION_SERVICE) as NotificationManager)
                .createNotificationChannel(channel)
        }
    }

    companion object{
        private const val CHANNEL_NAME = "chlqudco qudtls"
        private const val CHANNEL_DESCRIPTION = "chlqudco qudtls Ehfcn"
        private const val CHANNEL_ID = "chlqudcoID"
    }

	-CHANNEL_NAME은 앱 정보에 들가면 나오는거, 나머지 2개는 별 쓸모 없고

            

Glide 사용법
1. 의존성 추가
2. Glide.with(컨텍스트).load(주소).into(이미지뷰)
- 썸네일이란걸 미리 보여줄 수도 있음
-공식 문서에 기능 존나 많이 있음



- swiperefreshlayout
	- 위로 댕기면 새로고침 되는 레이아웃
	- 1. 의존성 추가
	- 2. xml에 쳐 넣어
	- 3. kt에서 이벤트 설정


- EditText 미세 팁
	- 밑줄 없애기 : 백그라운드 지정
	- elevation 설정하면 위로 올라와 보임
	- ime옵션과 kt의 이벤트?를 맞추셈
		- EditText
           		 .setOnEditorActionListener { editText, actionId, event ->
                		if (actionId == EditorInfo.IME_ACTION_SEARCH) {}
	- drawableStart하면 맨 앞에 드로어블 넣을 수 있음
		- 글자랑 띄우려면 드로어블패딩



- CardView
	- 카드 모양으로 보여줄 수 있는 뷰
	- cardCornerRadius 로 얼마나 깎을건지 지정

- TextView
	- 그림자도 줄 수 있음, shadowDx, Dy, Radius, Color 등등




- LoadingShimer
	- 페북에서 만든 로딩 대기?창
	- 글자 반짝반짝같은 응용도 가능
	- 1. 의존성 추가
	- 2. xml로 영역? 만들기, ShimmerFrameLayout입니당, 안에 레이아웃 하나 넣기
	- 3. 아이템을 최대한 간단?하게 만들기
	- 4. include 졸라게 하기
	- 5. kt에서 적절할때 쉬머 비져블 없애기


- 모션 레이아웃
	- 컨스트 레이아웃의 서브 클래스
	- 프레임 레이아웃에 넣는걸 배움
	- 컨스트레이아웃으로 만들기
		- 다 만들고 모션레이아웃으로 변경
		- 그럼 xml파일이 한개 생김
		- 컨스트레인트 셋에 할일 추가가능
	- 원하는 때에 연필모양   크리에이트 컨스트레인트 
	- 드래그 이벤트 걸려면 손가락 모양 터치 후 스와이프 핸들러
	- 모션 레이아웃 끼리 연결? 링크? 가능
		- 프래그먼트 kt 파일에서 모션 레이아웃에 setTrans리스너 달고 체인지에서 연결 
	- 위치 조절은 translation속성 이용 

	- 터치를 흘려주는 이벤트는 커스텀 모션 레이아웃으로 만들어야함
		- hitRect를 이용 
		- 제스쳐 리스너도 이용, ㅈㄴ 어려워 머야
	- 애니메이션 조절 하는 법
		- 유니티 마냥 시간 초 조절하면서 시계모양 눌러서 애드 어트리뷰트 하기
		- 그러면 키 어트리뷰트가 생김
		- 키포지션 주면 커짐, 커브 생기는거 ㅈ같으면 curveFit linear로 주기



- 액티비티에서 프래그먼트의 함수 호출
	- 서포트프래그매니저.프래그먼츠.find{it is 원하는 프래그먼트}?.let{
		(it as 원하는 프래그먼트).원하는 함수()
	}



