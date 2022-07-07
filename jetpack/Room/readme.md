- SQLite
  - 임베디드 관계형 데이터베이스 관리 시스템
  - c언어로 작성됨, 애플도 사용중

- Room
- 고수준의 DB 인터페이스 제공

- Repository
	- 앱에서 사용하는 모든 데이터 소스를 직접 처리하기 위해 필요한 모든 코드 포함
	- 이 코드를 레포에서 담당함으로 UI컨트롤러나 뷰모델이 데이터 소스 코드를 갖지 않게 해줌

- DAO
	- 레포지터리가 필요로 하는 SQL문(추가, 조회, 변경, 삭제)을 실행
	- @Dao위에 적고 인터페이스 생성
	- 함수 위에 @Query("SELECT * FROM tableName")
	- 인자 참조하려면 : 변수
	- @Insert, @Delete 다 됨
	- 반환 값은 처리된 행의 갯수

- Entity
	- 테이블의 스키마를 정의하는 클래스
	- 테이블 이름, 열 이름, 데이터 타입, 기본키 등등을 정의
	- DB 테이블은 각각 하나의 엔티티 클래스와 연관
	- @Entity(tableName = "asdasd")
	- @PrimaryKey(autoGenerate = true)
	- @ColumnInfo(name = "asdddd")
	- 외래 키에도 어노테이션 써야함


- DB클래스
	- RoomDatabase를 상속받아 클래스 만들기
	- 클래스 위에 @Database(entities = [Entity클래스::class], version = 1)
	- 안의 함수는 걍 Dao상속받는 abstract 함수 하나만 있으면 됨

- 인 메모리 DB
	- 룸은 인메모리 DB도 지원함
	- 메모리에만 존재해서 앱이 종료되면 사라짐
	- 왜쓰지..?

- 아래의 DB Inspector도구 창을 보면 실행 중인 앱의ㅣ DB를 조회할 수 있다,.

- 사용법
	- 1. gradle에서 id 'kotlin-kapt'
	-	imple : 안드x.룸:룸-런타임:버전
	-	kapt : 안드x.룸:룸-컴파일러:버전'

	- 2. 엔터티 클래스 생성
		- 무슨 내용을 담을건지 잘 결정(기본키두)

	- 3. DAO 인터페이스 생성
		- 예시봐!		

	- 4. Room DB abstract 클래스 구현

	- 5. 레포지터리 클래스 추가
		- 패캠에선 없었던거 같음
		- 결과값 받는 클래스
