- 상태 저장
	- 백그라운드에 있는 앱은 리소스가 부족할 때 종료될 수 있다
	- 복귀 시킬 때 종료된 앱은 새로운 프로세스로 다시 시작한다
	- 앱은 백그라운드에 있을 때와 동일한 상태가 되어야 하므로 상태 데이터를 저장 및 복원해야 함
	- viewModel을 사용하는 경우 ViewModel 상태 저장 모듈을 사용하면 된다

- SavedStateHandle
	- 상태 저장의 핵심 클래스, ViewModel 인스턴스의 상태를 저장하고 복원하는데 사용
	- Map 형식으로 저장함
	- 뷰모델의 생성자로 위 클래스를 받아야 함

- 상태 저장
	- 클래스.set(키, 값)

- 상태 복원
	- 클래스.get(키)
	- LiveData는 getLiveData로 복원할 수 있다

- 유용한 함수
	- contains, remove, keys 등등

- 구현
1. 의존성 추가

```
    implementation 'androidx.savedstate:savedstate:1.1.0'
    implementation 'androidx.lifecycle:lifecycle-viewmodel-savedstate:2.4.1'
```

2. ViewModel 클래스 재 정의

```
class MainViewModel(private val savedStateHandle: SavedStateHandle) : ViewModel()
```

3. 뷰모델 다시 생성

```
val factory = SavedStateViewModelFactory(it, this)
            viewModel = ViewModelProvider(this, factory).get(MainViewModel::class.java)
```

- 뭔가 빠진 느낌?

