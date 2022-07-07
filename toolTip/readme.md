- 1. 안스 프로그램 램 사용량 설정을 조절할 수 있다, 너무 렉걸리면 설정하기(폰 램 얘기 아님;)
	- File -> Settings -> System Settings -> Memory Settings 에서 힙사이즈 늘리기

- 2. 자동 import 
	- File -> Settings -> Editor -> General -> Auto Import에서 걍 다 체크;
	- 알트 앤

- 3. 모든 단축키 보기
	- Help -> Keymap Reference

- 4. 매개변수 정보 보기
	- 컨트롤 P

- 5. 코드 한꺼번에 접거나 펴기
	- 컨트롤 쉬프트 +or-

- 6. API 문서? 보기
	- 컨트롤 큐

- 7. 코드 스타일 변경
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
