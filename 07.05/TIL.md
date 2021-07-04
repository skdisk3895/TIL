## 안드로이드에서 Java 파일과 xml 파일 연결시키기

```java
setContentView(R.layout.xml파일이름);
```

## 실행 딜레이 시키기

```java
	Handler handler = new Handler();
	handler.postDelayed(new Runnable()  {
		public void run() {
            // 시간 지난 후 실행할 코딩
		}
	}, 500); // 0.5초후
```

## 앱이 처음 시작할 때 다른 액티비티를 먼저 실행하고 싶은 경우

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.phonehub">

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.Phonehub">
        <activity android:name=".IntroActivity">  <!--다른 액티비티로 바꿈-->
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
        <activity android:name=".MainActivity" />  <!--반드시 MainActivity가 있다는 것을 알려줘야 한다.-->
    </application>

</manifest>
```

기존 `MainActivitiy`가 있던 자리를 `다른 액티비티`로 교체하고 MainActivity는 `아래에서 자바파일이 있다는 것을 반드시 알려줘야 한다.` 만약 그렇지 않으면 `앱이 팅기게 된다`
