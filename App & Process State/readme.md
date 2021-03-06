- 앱과 리소스
	- 앱은 프로세스로 실행되며 여러 컴포넌트로 구성된다
	- 모바일 환경은 데스크톱에 비해 제한된 리소스(특히, 메모리)를 고려해야 한다
	- 따라서 안드로이드는 앱의 프로세스와 모든 컴포넌트의 생명주기와 상태를 전적으로 통제한다
	- 따라서 생명주기 모델을 잘 이해하며 개발해야 한다
	- 또한 생명주기 변화에 대한 대처 방법도 잘 수립해야 한다
	- 장치의 자원이 한계에 다다를 경우 안드로이드는 앱을 중단시킬 수 있다
	- 중단 순서는 우선순위와 상태를 모두 고려한다
	- 모든결 고려해서 importance hierarchy를 생성한 뒤 낮은 순으로 중단시킨다

- 안드로이드 프로세스 상태
	- 앱은 프로세스로 실행되고 컴포넌트로 구성된다
	- 프로세스는 다섯 가지 중 하나의 상태가 될 수 있다
		- foreground, visible, service, background, empty
	
- foreground 프로세스
	- 화면으로 보여지고 사용자와 상호작용하는 가장 높은 수준의 우선순위를 갖는 프로세스
	- 5개의 조건중 하나 이상을 충족해야 한다
		- user와 현재 상호작용 중인 액티비티를 호스팅한다
		- user와 현재 상호작용 중인 액티비티에 연결된 서비스를 호스팅한다
		- 이하 생략

- Visible 프로세스
	- 화면으로 볼수는 있지만 상호작용은 하지 않는 액티비티
	- 화면 일부를 다른 액티비티 (대화상자) 로 실행하면서 가리는 경우
	
- Service 프로세스
	- 이미 시작되어 현재 실행 중인 서비스를 포함하는 프로세스

- Background 프로세스
	- 유저가 화면으로 볼 수 없는 액티비티를 포함하는 프로세스
	- 우선순위가 낮아서 메모리 부족할 때 중단될 가능성이 크다
	
- Empty 프로세스
	- 앱을 실행시키진 않지만 메모리에 남아있는 애
	- 문 연 채로 승객을 기다리는 버스를 예로 들 수 있음
