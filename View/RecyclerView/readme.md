- RecyclerView
	- 스크롤 가능한 데이터 리스트를 사용자에게 제공
	- ListView 보다 더 많은 장점이 있다
		- 뷰를 관리하는 방법이 훨씬 효율적
		- 기존 뷰가 화면에서 벗어났을 때 그것을 재사용한다.
		- 성능 향상과 리소스를 줄여준다.
	- 세가지 레이아웃 매니저를 선택할 수 있다
	- LinearLayoutManager
		- 리스트 항목이 수평 또는 수직으로 나타난다
	- GridLayoutManager
		- 리스트 항목이 격자 형태로 나타난다.
	- StaggeredGridLayoutManager
		- 일정하지 않은 격자 형태로 나타난다.
	- 필요에 따라 커스텀 레이아웃 매니저를 구현할 수 있다.
	- 리사이클러 뷰의 각 항목은 ViewHolder 클래스의 인스턴스로 생성된다
	- 어댑터가 필요하다
		- 데이터와 리사이클러뷰간의 중개자 역할을 한다

- 리사이클러뷰 어댑터
	- 최소 아래 3개의 함수를 궇ㄴ해야 한다
	- getItemCount()
		- 리스트에 보여 줄 항목의 개수를 반환	
	- onCreateViewHolder()
		- 초기화된 ViewHolder 객체를 생성하고 반환한다.
		- XML 레이아웃 파일을 inflate 하여 생성된다
	- onBindViewHolder()
		- 뷰홀더 객체와 인덱스 값을 인자로 받는다
		- 지정된 항목의 데이터를 뷰에 넣은 후 ViewHolder 객체를 반환한다








