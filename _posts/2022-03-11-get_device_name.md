---
title:  "[Android] Device Name 가져오기"
excerpt: "Android Device Name 가져오기"

categories:
  - Android
tags:
  - Android
last_modified_at: 2022-03-11T22:40:00-05:00
---

# [Android] Device Name 가져오기
Build.java에 저장되어있는 정보를 사용한다.

## Source Code
``` kotlin
fun getDeviceModel(): String {
    return String.format("BRAND:%s MODEL:%s", Build.BRAND, Build.MODEL)
}
```

## 실행결과
``` kotlin
@@@@: getDeviceModel: BRAND:samsung MODEL:SM-T975N
```

참고) Build.java code를 보면 ro.build의 값을 가져와서 리턴해주는것을 알 수 있다.
해당 정보는 adb 명령어를 통해 확인할 수도 있다.

``` kotlin
adb shell getprop
``` 
Build.java code)

``` kotlin
public class Build {
    private static final String TAG = "Build";

    /** Value used for when a build property is unknown. */
    public static final String UNKNOWN = "unknown";

    /** Either a changelist number, or a label like "M4-rc20". */
    public static final String ID = getString("ro.build.id");

    /** A build ID string meant for displaying to the user */
    public static final String DISPLAY = getString("ro.build.display.id");

    /** The name of the overall product. */
    public static final String PRODUCT = getString("ro.product.name");

    /** The name of the industrial design. */
    public static final String DEVICE = getString("ro.product.device");
    
    ...
}
``` 

