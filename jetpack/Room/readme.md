- 앱의 일시적인 생명주기를 고려했을 때, 영속적인 데이터 저장이 매우 중요함
- 관계형 데이터베이스를 이용

- 테이블
	- 데이터베이스에 필수적인 데이터 구조 제공
	- 특정 타입의 정보를 저장하도록 설계
		- ex) 고객 테이블에는 이름, 주소 전화번호 등의 값들이 있음
	- 하나의 데이터베이스에서는 테이블 이름이 중복되면 안됨

- 데이터베이스 스키마
	- 테이블에 저장된 데이터의 특성을 정의
		- ex) 고객 테이블의 이름 필드는 20자 이내의 문자열이여야 함
	- DB 전체 구조와 DB에 포함된 테이블 간의 관계를 정의하는 데도 사용

- 열(Column)
	- 세로줄
	- 해당 테이블의 데이터 필드를 나타냄
		- ex) 고객 테이블의 이름, 주소, 전화번호 등
	- 각 열은 특정 데이터 타입으로 정의

- 행(Row)
	- 가로줄
	- 레코드 하나를 가르킴
		- ex) 고객 테이블의 최병채 고객 전체 내용
	- 엔트리 라고도 함

- 기본키
	- Primary Key
	- 테이블은 각 행을 고유하게 식별가능하게 해주는 값이 필요함
	- ex) 고객 테이블의 주민번호..? 고객 번호?

- SQLite 관계형 데이터베이스
	- 크기가 작아서 모바일용 RDBMS로 적합함
	- 안드로이드와 ios 모두 사용중
	- c언어로 만들어짐
	- 키워드가 많지 않아 배우기 쉬움

- Room Persistence Library
	- SQLite 사용상의 문제를 해결하기 위해 Room을 만듬
	- Jetpack에 포함되어있음 

- Repository
	- 앱에서 사용하는 모든 데이터 소스를 직접 처리하기 위해 필요한 모든 코드를 포함
	- 따라서 데이터 소스를 직접 사용하는 코드를 UI와 뷰모델에서 갖지 않도록 함

- Room DB
	- SQLite DB에 대한 인터페이스 제공
	- Repository가 DAO(Data Access Object)를 사용하게 해줌
	- 앱은 하나의 Room DB 인스턴스만 가질 수 있음
	- companion object로 싱글턴 구현하면 편함

@Database(entities = [History::class, Review::class], version = 2)
abstract class AppDatabase : RoomDatabase() {
    abstract fun historyDao(): HistoryDao
    abstract fun reviewDao(): ReviewDao
}

- DAO
	- DB에 데이터를 추가, 조회 등 Repository가 필요로 하는 SQL문을 포함
	- 이 SQL은 Repository에서 호출되는 함수와 연결되어 쿼리를 실행함
	- 반환 값은 처리된 행의 갯수
@Dao
interface HistoryDao {

    @Query("SELECT * FROM history")
    fun getAll(): LiveData<List<History>>

    @Insert
    fun insertHistory(history: History)

    @Query("DELETE FROM history WHERE keyword = :keyword")
    fun delete(keyword: String)

    @Delete
    fun deleteCustomer(Customer...coutomers)
}


- Entity
	- DB 테이블의 스키마를 정의하는 클래스
	- 테이블 이름, 열 이름 및 타입, 기본키를 정의
	- DB테이블은 각각 하나의 엔터티 클래스와 연관된다
@Entity
data class Customer(
    @PrimaryKey(autoGenerate = true) val customerId: Int,
    @ColumnInfo(name = "age") val age: Int
)

- 각각은 서로 상호작용 한다
	- 레포는 Room DB와 상호작용 하여 DB 인스턴스를 얻으며, 이 인스턴스는 DAO 인스턴스의 참조를 얻는데 사용
	- 레포는 엔터티 인스턴스를 생성하고 데이터를 채운뒤 연산을 위해 DAO에 전달한다
	- DAO는 Room DB와 상호작용하여 DB작업을 시작하고 결과를 처리한다
	- Room DB는 SQLite DB와 상호작용하여 쿼리를 요청하고 결과를 받는다

- 인 메모리 DB
	- 룸은 인메모리 DB도 지원함
	- 메모리에만 존재해서 앱이 종료되면 사라짐
	- 왜쓰지..?

- DB Inspector 도구 창을 보면 실행 중인 앱의ㅣ DB를 조회할 수 있다,.

- 사용법
	- 1. gradle에서 id 'kotlin-kapt'
	- imple : 안드x.룸:룸-런타임:버전
	- kapt : 안드x.룸:룸-컴파일러:버전'

	- 2. 엔터티 클래스 생성
		- 무슨 내용을 담을건지 잘 결정(기본키두)

	- 3. DAO 인터페이스 생성

	- 4. Room DB abstract 클래스 구현
