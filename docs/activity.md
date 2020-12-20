## How to create and call another activity
### android.content.Intent Class Information

[Office Docs link for android.content.Intent](https://developer.android.com/reference/android/content/Intent)

Every activity is in a separated class. An intent is an abstract description of an operation to be performed.

In order to create a new activity, first you need to create a class. Then, use startActivity() method to open you created activity.

startAcitivity() method takes an Intent object as parameter.

``` java
// This is under MainActivity Class
import android.content.Intent;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    public void myButtonOnClicked(View v) {
        Intent intent = new Intent(this, MySecondActivity.class);
        startActivity(intent);
    }
}
```

---

## How to change default activity (Which activity is the main activity)
1. Go to AndroidManifest.xml, it is in "{project folder}\app\src\main" folder.
2. ```action``` tag and ```category``` tag in ```intent-filter``` block will determine which activity run first.
   ``` xml
       <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.Intent">
        <activity android:name=".MySecondActivity"></activity>
        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
   ```

---

## How to change each acivity title
``` java
// In .java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        setTitle("First Activity");   // Set current activity title
    }
}
```

---

## How to change APP Label
```android:label``` changes the label of the APP.
``` xml
<!-- In AndroidManifest.xml -->
<application
    android:allowBackup="true"
    android:icon="@mipmap/ic_launcher"
    android:label="@string/app_name"
    android:roundIcon="@mipmap/ic_launcher_round"
    android:supportsRtl="true"
    android:theme="@style/Theme.Intent">
    <activity android:name=".MySecondActivity"></activity>
    <activity android:name=".MainActivity">
        <intent-filter>
            <action android:name="android.intent.action.MAIN" />
            <category android:name="android.intent.category.LAUNCHER" />
        </intent-filter>
    </activity>
</application>

<!-- In string.xml -->
<resources>
    <string name="app_name">MyIntent</string>
</resources>
```

![App Label](https://tonywang1027.github.io/Android-Development-Logs/imgs/App Label.png)

---

## How to set an activity as child activity of an parent
```android.parenActivityName``` set this activity as a child of parent activity
``` xml
<application
    android:allowBackup="true"
    android:icon="@mipmap/ic_launcher"
    android:label="@string/app_name"
    android:roundIcon="@mipmap/ic_launcher_round"
    android:supportsRtl="true"
    android:theme="@style/Theme.Intent">
    <activity
        android:name=".MySecondActivity"
        android:parentActivityName=".MainActivity" />
    <activity android:name=".MainActivity">
        <intent-filter>
            <action android:name="android.intent.action.MAIN" />
            <category android:name="android.intent.category.LAUNCHER" />
        </intent-filter>
    </activity>
</application>
```

---

## How to pass valuable from an activity to another activity
**Using Intent**

[putExtra method (Official)](https://developer.android.com/reference/android/content/Intent#putExtra(java.lang.String,%20android.os.Parcelable))

``` java
// In MainActivity.java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        setTitle("First Activity");
    }

    public void myButtonOnClicked(View v) {
        Intent intent = new Intent(this, MySecondActivity.class);
        EditText editText = findViewById(R.id.editText);   // Get text from editText widget
        intent.putExtra("key", editText.getText());   // Passing valuable to another activity
        // First argument is a key(or name)
        // Second argument is the actual value

        startActivity(intent);
    }
}
```

``` java
// In MySecondActivity.java
public class MySecondActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_my_second);

        Intent intent = getIntent();   // Get intent
        String message = intent.getStringExtra("key");   // Get string from MainActivity.java
        TextView textView = findViewById(R.id.textView);
        textView.setText(message);   // Set string to textView
    }
}
```
