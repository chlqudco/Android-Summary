- 앱 간에 데이터를 공유하는 메커니즘을 구현
- 어떤 앱도 자신의 내부 데이터 사용을 다른 앱에 제공할 수 있음
- 해당 데이터를 추가, 삭제, 조회하는 능력을 갖는 콘텐트 프로바이더를 구현
- 데이터의 사용은 URI를 통해 제공됨
- 데이터는 파일 또는 DB 형태로 공유될 수 있음
- ex) 연락처, 미디어 파일
- 현재 사용 가능한 콘텐트 프로바이더는 콘텐트 리졸버를 사용해서 찾을 수 있음