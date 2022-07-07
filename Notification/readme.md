- 앱이 실행되고 있지 않거나 백그라운드 상태일 때, 사용자에게 메세지를 전달하는 방법
- 패캠 알림 앱에서 자세히 설명해주고 있다. 

- 로컬 알림 (local 알림)
	- 실행 중인 앱에서 만드는 알림

- 원격 알림 (romote 알림)
	- 원격 서버에서 만들어서 장치에 전송하는 알림
	- FCM을 이용해서 쉽게 테스트 해볼 수 있다.

- 알림에는 버튼이 있을 수 있고 특정 행동을 할수 도 있다.

- 알림을 받기 위해 알림 채널을 만들어야 한다.
	-식별id, 채널이름, 채널설명으로 구성되어 있음

- 1. 노티매니저 초기화
private var notificationManager: NotificationManager? = null
notificationManager = getSystemService(Context.NOTIFICATION_SERVICE) as NotificationManager

- 2. 채널 생성
val channel = NotificationChannel(id, name, importance)
notificationManager?.createNotificationChannel(channel)

- 더 많은 옵션을 줄 수도 있다.
- 또한 채널 삭제도 코드상에서 가능하다
deleteNotificationChannel(channelID)

- 로컬 알림 생성 방법
	- 그냥 만들면 됨. 노티 빌더 이용해서 노티 만든뒤 notify(id,노티)

- 앱 클릭시 특정 액티비티 시작하게 하는법
	- 당연하지만 인텐트를 사용해야함
	- 근데 PendingIntent에 등록해야함
	- PendingIntent는 인텐트를 다른 앱에 전달할 수 있으며, 전달받은 앱이 향후에 해당 인텐트를 수행할 수 있게 해줌

- 오류 발생
	- pendingIntent의 마지막인자로 FLAG_UPDATE_CURRENT를 지정한 경우 오류가 발생
	- Targeting S+ (version 31 and above) requires that one of FLAG_IMMUTABLE or FLAG_MUTABLE be specified when creating a PendingIntent.
	- API 31이상 부터는 저 플래그를 달아야 된다고 해서 바꿔줌.
	- FLAG_IMMUTABLE로 바꿔서 대충 해결은 했는데 찝찝

- 알림에 액션을 추가하면 또 다른 방법으로 액티비티를 시작시킬 수 있음
	- val action: Notification.Action = Notification.Action.Builder(icon,"Open", pendingIntent).build()

- 알림이 너무 많아지면 보기 힘들 수 있으니, 그룹으로 묶을 수 있다.
	- ex) 카카오톡 채팅 알림

- 직접 응답 기능 (direct reply)
	- 카톡 바로 답장 기능처럼 알림에서 텍스트를 전달할 수 있다.
	- RemoteInput 클래스가 핵심 요소임
	- 알림 어떻게 끄지..
