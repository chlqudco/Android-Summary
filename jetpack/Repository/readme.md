- Repository
	- ViewModel이 하나 이상의 외부 소스로부터 데이터를 얻는다면, 처리하는 코드를 분리해야 한다
		- 외부 소스는 DB나 API 같은 웹서비스를 말함
	- 이런 코드를 별도의 Repository 모듈에 둘 것을 권장한다
	- 다양한 데이터 소스와의 인터페이스를 담당하며, 데이터가 모델에 저장될 수 있도록 ViewModel에도 인터페이스를 제공한다.
![img](https://user-images.githubusercontent.com/68932465/178423194-825f5e8d-0e92-4bec-a0d8-020481f8a25c.png)
