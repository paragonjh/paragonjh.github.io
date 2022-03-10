---
title:  "[Android] 부팅 후 앱 자동 실행"
excerpt: "Android 부팅 후 앱 자동 실행"

categories:
  - Android
tags:
  - Android
last_modified_at: 2022-03-10T22:02:00-05:00
---

# [Android] 부팅 후 앱 자동 실행
안드로이드 단말에서 부팅 완료 된 후에 자동으로 특정 어플리케이션을 실행시키는 방법에 대해 공유하고자 합니다.

아래의 코드를 적용 후 기기를 재부팅시켜주면 구동 후 앱이 자동적으로 실행되는 것을 볼 수 있습니다.

* 잠금화면이 풀려있어야 정상적으로 실행되고 잠금화면이 설정되었다면 잠금 해제 시에 실행 됩니다.

## 1) Android Manifest 수정

1) 아래 2개의 Permission을 Android Manifest에 추가한다.

``` xml
<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW"/>
```

2) application tag 안에 receiver를 추가한다.

``` xml
<receiver
        android:name=".AutoRun"
        android:enabled="true"
        android:exported="true"
        android:permission="android.permission.RECEIVE_BOOT_COMPLETED" >
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED" />
            <category android:name="android.intent.category.DEFAULT" />
        </intent-filter>
</receiver>
```

##2) BroadcastReciever class 만들기
Android Booting이 완료됨을 알수 있도록 BroadcastReciever class 를 생성한다.

``` kotlin
class AutoRun : BroadcastReceiver() {
    override fun onReceive(context: Context, intent: Intent) {
        if (intent.action == "android.intent.action.BOOT_COMPLETED") {
            val it = Intent(context, SplashActivity::class.java)
            it.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK)
            context.startActivity(it)
        }
    }
}
```

##3) Permission 획득 요청
Android 10 이상은 Draw Overlay Permission이 필요하다.
첫번째 시작 activity에 하기의 code를 추가 후 onCreate시 권한획득을 확인한다.

``` kotlin
private fun requestPermission() {
    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
        if (!Settings.canDrawOverlays(this)) {
            val intent = Intent(
                Settings.ACTION_MANAGE_OVERLAY_PERMISSION,
                Uri.parse("package:" + this.packageName)
            )
            startActivityForResult(intent, 232)
        } else {
            //Permission Granted-System will work
        }
    }
}
```


