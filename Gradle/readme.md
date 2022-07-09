- Gradle
	- 안드로이드 스튜디오의 그래들은 앱 프로젝트를 컴파일 하고 실행하는데 필요한 일을 해줌
	- 자동화된 빌드 시스템이며, 빌드 구성 파일을 통해 프로젝트 빌드가 구성되고 관리되게 해줌
	- 독립적인 환경이면서 플러그인을 통해 다른 환경에 통합될 수 있다
		- 안드로이드 스튜디오는 안드로이드 스튜디오 플러그인을 통해 그래들이 통합되어 있음
		- 따라서 안스가 설치 안되어 있어도 별도로 명령행 도구를 사용하면 빌드할 수도 있음
	- 프로젝트를 빌드하기 위한 구성 규칙은 Groovy 언어 기반의 스크립트로 그래들 빌드 파일에 선언

- Gradle과 안드로이드 스튜디오
	- 중요한 기능을 정리해 본다.
	
1. 합리적인 디폴트
	- 그래들은 CoC 개념을 구현하고 있다.
	- 개발자가 빌드 파일의 설정을 변경하지 않았을 때 기본 설정으로 사용됨
	- 개발자가 필요한 최소한의 구성만으로 빌드가 수행될 수 있다는 뜻
	- 디폴트 구성이 요구사항에 맞지 않을 때만 변경하면 되는 편리함을 제공

2. 의존성(Dependency)
	- 또 다른 중요한 그래들 기능
	- 안드로이드 스튜디오는 다른 모듈을 사용하기 위해 의존성을 선언해야만 함
	- 로컬 의존성 과 원격(remote) 의존성으로 분류됨
	- 로컬 : 컴퓨터의 로컬 파일 시스템에 있는 모듈을 참조함
	- 원격 : repository 라고 하는 원격 서버에 있는 모듈을 참조
	- 원격 의존성은 Maven이라는 또 다른 프로젝트 관리 도구를 사용해서 처리함

3. 빌드 변이
	- 그래들은 프로젝트의 빌드 변이(build variant) 지원을 제공함
	- 즉, 하나의 프로잭트로 여러 변형된 버전의 앱을 빌드할 수 있다
	- 안드로이드는 다양한 cpu 타입과 화면을 갖는 여러 장치에서 실행된다.
	- 가능한 한 많은 장치에서 앱이 실행되게 하려면 하나의 프로젝트를 서로 다른 변형된 버전의 앱으로 빌드할 필요가 있다

4. 매니페스트 항목
	- 프로젝트는 앱의 자세한 구성 정보를 갖는 매니페스트 파일을 갖고 있다. 
	- 많은 매니페스트 항목이 그래들 빌드 파일에 지정될 수 있고, 빌드될 때 매니페스트 파일로 자동 생성해 준다.
	- 빌드 변이 생성을 도와준다. 여러 요소를 각 빌드 변이마다 다르게 구성될 수 있게 해주기 때문

5. APK 서명
	- 입력된 서명 정보를 그래들 빌드 파일에 포함시키는 것도 가능하다

6. Proguard 지원
	- 자바 바이트 코드를 최적화하고 크기를 줄여준다
	- 또한 reverse engineering을 통한 소스 코드 해독을 어렵게 해준다
	- reverse engineering : 컴파일된 바이트 코드 분석을 통해 앱의 로직을 알아볼 수 있는 방법
	- 그래들에서 Proguard를 실행할 것인지 여부를 제어할 수 있다 

- 최상위 수준의 그래들 빌드 파일
	- 각 프로젝트는 하나의 최상위 그래들 빌드 파일을 포함한다. Project 수준의 gradle
	- 대부분의 경우에 이 빌드 파일은 변경하지 않아도 된다

- 모듈 수준의 그래들 빌드 파일
	- 프로젝트는 하나 이상의 모듈로 구성되며, 각 모듈은 자신의 그래들 빌드 파일이 있다. 앱 수준의 gradle
	- plugins{} : 어떤 플러그인을 사용할건지 선언
	- android{} : 빌드 할 떄 사용할 SDK와 빌드 고구의 버전을 정의
	- defaultConfig{} : 빌드하는 동안 해당 모듈의 매니페스트 파일로 생성되는 요소를 정의
	- buildTypes{} : 앱의 릴리스 버전이 빌드 될때 Proguard 사용 여부와 실행 방법 정의
	- compileOptions{}, kotlinOptions{} : 프로젝트르 ㄹ빌드 할 때 사용되는 자바 컴파일러의 버젼 지정
	- dependencies{} : 앱 모듈의 로컬과 원격 의존성을 나타냄, app 모듈을 빌드 할 때 필요한 라이브러리 지정

- 빌드 파일에 미리 서명 설정을 구성할 수 있다.
	- signingConfigs섹션에 작성
```
signingConfigs{
	release {
		storeFile file("keystore.relese")
		storePassword "키스토어 비밀번호"
		keyAlias "키 alias"
		keyPassword "키 비밀번호"
	}
}
```
	- 이 외에도 여러 방법이 있음