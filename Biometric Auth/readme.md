- 생체 인증
	- 현재 대부분의 장치는 지문인식 기능을 제공함
	- 물론 지문인식 말고도 얼굴, 비밀번호, PIN 등 많은 인증 방식이 있음
	- 앞으론 얼굴인식도 보편화 될것이므로 구글은 앱의 인증기능을 통틀어 생체 인증이라고 부름
	
- BiometricPrompt
	- 생체인증은 BiometricPrompt가 핵심 클래스임
	- 모든걸 알아서 처리해준다고 보면 됨 = 통일된 UI를 제공
	- 5회 실패시 인증 불가도 자동 제공 

1. 매니페스트에 퍼미션 축자하기  
```
 <uses-permission android:name="android.permission.USE_BIOMETRIC"/>
```

2. 장치에 잠금장치와 지문이 등록되어 있는지 확인
```
    private fun checkBiometricSupport(): Boolean {
        val keyguardManager = getSystemService(Context.KEYGUARD_SERVICE) as KeyguardManager
        
        //잠금 화면을 안한 경우
        if (!keyguardManager.isKeyguardSecure){
            notifyUser("잠금 설정이 되어 있지 않습니다")
            return false
        }
        
        //권한이 없는경우
        if (ActivityCompat.checkSelfPermission(this,Manifest.permission.USE_BIOMETRIC) != PackageManager.PERMISSION_GRANTED){
            notifyUser("지문 인식 권한이 없습니다")
        }
        
        return packageManager.hasSystemFeature(PackageManager.FEATURE_FINGERPRINT)
    }
```

3. 생체인증 대화상자 구성을 위한 인증 콜백 함수 구현
	- 인증의 성공 실패 여부를 앱에 전달해줌
```
    private val authenticationCallback: BiometricPrompt.AuthenticationCallback
        get() = object : BiometricPrompt.AuthenticationCallback(){
            
            override fun onAuthenticationError(errorCode: Int, errString: CharSequence?) {
                notifyUser("에러 발생 : $errString")
                super.onAuthenticationError(errorCode, errString)
            }

            override fun onAuthenticationHelp(helpCode: Int, helpString: CharSequence?) {
                super.onAuthenticationHelp(helpCode, helpString)
            }

            override fun onAuthenticationFailed() {
                super.onAuthenticationFailed()
            }

            override fun onAuthenticationSucceeded(result: BiometricPrompt.AuthenticationResult?) {
                notifyUser("인증에 성공했습니다")
                super.onAuthenticationSucceeded(result)
            }
            
        }
```

- 생체 인증 프로세스는 앱과 독립적으로 수행됨.
	- 따라서 인증 작업 취소 방법을 CancellationSignal로 구현해야 함
```
    private var cancellationSignal: CancellationSignal? = null
    
    private fun getCancellationSignal(): CancellationSignal{
        cancellationSignal = CancellationSignal()
        cancellationSignal?.setOnCancelListener { 
            notifyUser("취소됐습니다.")
        }
        return cancellationSignal as CancellationSignal
    }
```

5. 생체 인증 시작하기
```
    fun authenticateUser(view: View){
        val biometricPrompt = BiometricPrompt.Builder(this)
            .setTitle("생체 인증")
            .setSubtitle("계속 하려면 인증해주세요")
            .setDescription("이 앱은 생체인증이 필요합니다")
            .setNegativeButton("취소", this.mainExecutor, DialogInterface.OnClickListener { dialog, which -> 
                notifyUser("인증을 취소했습니다")
            }).build()
        
        //mainExecutor는 메인쓰레드를 말하는 거임
        biometricPrompt.authenticate(getCancellationSignal(), mainExecutor, authenticationCallback)
    }
```
