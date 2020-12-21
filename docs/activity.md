## How to create an activity from sketch (not using activity_main.xml file)

``` java
public class MainActivity extends Activity {
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        // Create a LinearLayout
        final LinearLayout layout = new LinearLayout(this);
        layout.setOrientation(LinearLayout.VERTICAL);   // Set screan to vertical
        setContentView(layout);   // Add layout to content view

        // Create buttons
        final Button btn1 = new Button(this);
        btn1.setText(R.string.btn1_text);
        final Button btn2 = new Button(this);
        btn2.setText(R.string.btn2_text);
        final Button btn3 = new Button(this);
        btn3.setText(R.string.btn3_text);
        final Button btn4 = new Button(this);
        btn4.setText(R.string.btn4_text);

        // Add these buttons into layout
        layout.addView(btn1);
        layout.addView(btn2);
        layout.addView(btn3);
        layout.addView(btn4);
    }
}
```

``` xml
<!-- string.xml -->
<resources>
    <string name="app_name">JavaCodedUI</string>
    <string name="btn1_text">Button#1</string>
    <string name="btn2_text">Button#2</string>
    <string name="btn3_text">Button#3</string>
    <string name="btn4_text">Button#4</string>
</resources>
```

``` xml
<!-- AndroidManifest.xml -->
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.firstemptyapp">

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.FirstEmptyApp">
        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
</manifest>
```

---

## How to create a circle button
1. Create a shape.xml file inside drawable folder
    ``` xml
    <!-- shape.xml -->
    <?xml version="1.0" encoding="utf-8"?>
    <shape xmlns:android="http://schemas.android.com/apk/res/android"
        android:shape="oval">
        <solid android:color="#99FFFF"/>
    </shape>
    ```
    android:shape="oval" - type of shape

    android:color - change the color of the shape

2. Code Part
   ``` java
   import android.app.Activity;
   import android.os.Bundle;
   import android.widget.Button;
   import android.widget.LinearLayout;
   public class MainActivity extends Activity {
       public void onCreate (Bundle savedInstanceState) {
           super.onCreate(savedInstanceState);

           final LinearLayout layout = new LinearLayout(this);
           layout.setOrientation(LinearLayout.VERTICAL);
           setContentView(layout);

           final Button btn1 = new Button(this);
           btn1.setBackgroundResource(R.drawable.shape1);   // Customize background color
           LinearLayout.LayoutParams LP_WW = new LinearLayout.LayoutParams(100, 100);
           btn1.setLayoutParams(LP_WW);

           layout.addView(btn1);
   ```
   ```LinearLayout.LayoutParams LP_WW = new LinearLayout.LayoutParams(100, 100);``` - set button width and height to 100dp.

---

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
