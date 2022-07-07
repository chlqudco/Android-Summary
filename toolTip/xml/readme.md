-버튼 클릭시 위로 올라오는 이벤트 업새기
	-stateListAnimator = "@null"

-가로로 늘어선 버튼 사이 여백 없애기
   -Horizontal_chainstyle = packed 

-뷰나 레이아웃들에 app:layout_constraint방향_웨이트 값을 지정하면 비율대로 나눈다.


-Edittext
	-입력완료 이벤트 : imeOptions
		-actionDone : 키보드 숨김
		-책 260쪽
	-자동 줄바꿈 : inputType 에 textMultiLine 으로

-이미지 버튼
	-투명배경 : background = color/transparent
	-크기 설정 : scaleType = 264쪽


- 스크롤뷰 : 스크롤생김
	- 안에 레이아웃을 추가해서 사용


- 폰트 저장하는법 
	- ttf파일 받아서 res폴더에 font폴더 새로 만들고 안에 넣기
	- xml가서 fontFamily = "@font/파일이름" 으로 적용


- dp
	- 해상도와 관계없이 동일한 크기
- sp	
	- 글씨..크기 전용?


- 클릭 이벤트 xml로 달기
	- onClick = "함수 이름"
	- 메인액티비티의 onClick이벤트는 v: View를 인자로 받아야됨
	- v.id 로 바로 아이디접근 가능
- 이미지 버튼
	- src로 이미지 고르기 R.drawable.~~~
	- 벡터 에셋으로 맘에 드는거 고리기


- 테이블 레이아웃
	- 격자 무늬로 배치할 수 있음, 계산기 같은 앱에 유용
	- 테이블로우 : 하나의 줄, 높이는 웨이트를 같은 값으로 주는것도 ㄱㅊ
	- 테이블 로우 안에 컴포넌트 넣으면 알아서 배치됨
	- 사이즈를 고르게 가져가게 하기 위해 태이블 레이아웃에 shrink컬럼스 = "*"를 주면 밖으로 안빠져나가고 고르게 나눠가짐


- 비율 주는 법
	- Ratio쓰고 자동완성 된거 선택 = "H or W, 1:3"
