- 원격 스토리지 서비스 (클라우드 스토리지)
	- 문서 제공자에 저장된 파일을 쉽게 앱에서 접근 가능하게 해줌
	- 사용자의 파일과 데이터를 저장
	- 따라서 구글은 Storage Access Framework를 소개

- SAF
	- 간단하게 말하면 걍 저장소 탐색? 기능
	- 사용하기 쉬운 UI를 제공
	- 인텐트를 사용해서 접근할 수 있다
	- ACTION_OPEN_DOCUMENT = 파일 선택 가능
	- ACTION_CREATE_DOCUMENT = 파일 새로 만들기 가능
	- 반환값은 파일의 Uri와 성공여부
	- 파일의 타입제한가능
		- intent.type = "image/*"

- 결과 처리하기
	- onActivityResult()로 반환됨
	- 결과 파일을 읽는 방법은 당연히 타입에 따라 다름
