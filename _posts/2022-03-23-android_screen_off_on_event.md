---
title:  "[Android] Screen On/Off 이벤트 수신, 상태 확인"
excerpt: "Screen On/Off 이벤트 수신, 상태 확인"

categories:
  - Android
tags:
  - Android
last_modified_at: 2022-03-23T22:17:00-05:00
---

# [Android] Screen On/Off 이벤트 수신, 상태 확인하기
Android는 화면이 켜지거나 꺼질 때 ACTION_SCREEN_ON, ACTION_SCREEN_OFF 인텐트를 브로드캐스트로 전달합니다. 
앱에서는 이 인텐트를 받아서 디바이스의 화면이 켜지는지, 꺼지는지 알 수 있습니다.

암시적(Implicit) 브로드캐스트 제한 정책으로, 타겟이 정해지지 않은, 암시적 인텐트는 Context로 등록된 리시버로만 전달됩니다. 
즉, AndroidManifest에 등록된 리시버는 인텐트를 받을 수 없게 됩니다. 이 정책은 Target API 26 이상인 앱에게만 적용됩니다.

따라서, ACTION_SCREEN_ON, ACTION_SCREEN_OFF 인텐트를 수신하려면 다음과 같이 Context.registerReceiver()으로 동적으로 등록해야 합니다.

## Code
```kotlin
class MainActivity : ComponentActivity() {
    private val screenDetectionReceiver = object : BroadcastReceiver() {
        override fun onReceive(context: Context?, intent: Intent?) {
            val action = intent!!.action
            Log.d("@@@@","screenDetectionReceiver receive: $action")
            when (action) {
                Intent.ACTION_SCREEN_ON -> {
                    Log.d("@@@@","ACTION_SCREEN_ON")
                }
                Intent.ACTION_SCREEN_OFF -> {
                    Log.d("@@@@","ACTION_SCREEN_OFF")
                }
            }
        }
    }
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        // BroadcastReceiver 등록
        val intentFilter = IntentFilter(Intent.ACTION_SCREEN_OFF)
        intentFilter.addAction(Intent.ACTION_SCREEN_ON)
        registerReceiver(screenDetectionReceiver, intentFilter)
    }

    override fun onDestroy() {
        super.onDestroy()
        // BroadcastReceiver 해제
        unregisterReceiver(screenDetectionReceiver)
    }
}
```

## 실행 결과
```
2022-03-23 22:00:03.745  D/@@@@: screenDetectionReceiver receive: android.intent.action.SCREEN_OFF
2022-03-23 22:00:03.747 D/@@@@: ACTION_SCREEN_OFF

2022-03-23 22:00:10.890 D/@@@@: screenDetectionReceiver receive: android.intent.action.SCREEN_ON
2022-03-23 22:00:10.890 D/@@@@: ACTION_SCREEN_ON
```