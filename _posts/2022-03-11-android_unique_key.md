---
title:  "[Android] Device 고유키 생성 방법"
excerpt: "Android Device 고유키 생성 방법"

categories:
  - Android
tags:
  - Android
last_modified_at: 2022-03-11T22:17:00-05:00
---

# [Android] Device 고유키 생성 방법
Device의 고유키를 생성하는 부분은 어느 플랫폼에서건 쉽지 않은 방법인것 같다.

다음은 Android에서 AndroidId를 기반으로 Device 고유키를 생성하는 방법에 대하여 공유하고자 한다.

참고) AndroidId는 공장초기화 시점에 생성된다고 한다. -> 공장 초기화를 하면 AndroidId가 변경된다.

## Source 설명
AndroidId를 바로 사용하지 않고 생성된 AndroidId를 MD5로 암호화하여 사용한다.


## Source Code
``` kotlin
private fun md5Encode(str: String): String? {
    var md5String: String? = ""
    md5String = try {
        val md: MessageDigest = MessageDigest.getInstance("MD5")
        md.update(str.toByteArray(charset("UTF-8")))
        val byteData: ByteArray = md.digest()
        val sb = StringBuffer()
        for (i in byteData.indices) sb.append(
            ((byteData[i] and 0xff.toByte()) + 0x100).toString(16).substring(1)
        )
        sb.toString()
    } catch (e: NoSuchAlgorithmException) {
        e.printStackTrace()
        null
    } catch (e: UnsupportedEncodingException) {
        e.printStackTrace()
        null
    }
    return md5String
}

@SuppressLint("HardwareIds")
fun getDeviceId(context: Context): String? {
    var deviceId: String? = ""
    val androidId: String = Settings.Secure.getString(
        context.contentResolver,
        Settings.Secure.ANDROID_ID
    )
    Log.d("@@@@", "androidId: $androidId")
    deviceId = md5Encode(androidId)
    return deviceId
}
```

## 실행 결과
``` kotlin
@@@@: androidId: b7a32de2265baea9
@@@@: deviceId: 400619492b3271a74577e76931
```