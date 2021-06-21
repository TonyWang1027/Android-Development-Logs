# Activity

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

## How to disable title bar for an Activity in XML
Go to res/values/themes/themes.xml
``` xml
<resources xmlns:tools="http://schemas.android.com/tools">
    <!-- Base application theme. -->
    <style name="Theme.EmptyProjectTest" parent="Theme.MaterialComponents.DayNight.NoActionBar">  <!-- NoActionBar will disable the title bar (action bar) -->
        <!-- Primary brand color. -->
        <item name="colorPrimary">@color/purple_500</item>
        <item name="colorPrimaryVariant">@color/purple_700</item>
        <item name="colorOnPrimary">@color/white</item>
        <!-- Secondary brand color. -->
        <item name="colorSecondary">@color/teal_200</item>
        <item name="colorSecondaryVariant">@color/teal_700</item>
        <item name="colorOnSecondary">@color/black</item>
        <!-- Status bar color. -->
        <item name="android:statusBarColor" tools:targetApi="l">?attr/colorPrimaryVariant</item>
        <!-- Customize your theme here. -->
    </style>
</resources>
```

---

## Instantiates a layout xml file into View object
```LayoutInflater``` is used to instantiate xml file into a java object
```inflate(int resource, ViewGroup root)``` Inflate a new view hierarchy from the specified xml resource.
``` java
// In TitleView.java
public class TitleView extends RelativeLayout {

    private final Button leftButton;
    private final TextView titleText;

    public TitleView(Context context, AttributeSet attrs) {
        super(context, attrs);

        LayoutInflater.from(context).inflate(R.layout.title, this);  // Instantiates title.xml file into a java object

        titleText = (TextView) findViewById(R.id.title_text);
        leftButton = (Button) findViewById(R.id.button_left);

        leftButton.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                // ((Activity) getContext()).finish();
                Log.d("DEBUG-C", "Button clicked");
            }
        });
    }
}

```

``` xml
<!-- In title.xml file (R.layout.title) -->
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="50dp"
    android:background="#ffcb05">

    <Button
        android:id="@+id/button_left"
        android:layout_width="80dp"
        android:layout_height="40dp"
        android:layout_centerVertical="true"
        android:layout_marginLeft="5dp"
        android:background="@android:color/black"
        android:text="@string/back"
        android:textColor="#fff" />

    <TextView
        android:id="@+id/title_text"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerInParent="true"
        android:text="@string/this_is_title"
        android:textColor="#fff"
        android:textSize="20sp" />

</RelativeLayout>
```

``` xml
<!-- In activity_main.xml file -->
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <!-- add title view into main activity xml -->
    <com.example.customwidget.TitleView
        android:id="@+id/title_view"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:onClick="widgetClicked"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent">

    </com.example.customwidget.TitleView>

</androidx.constraintlayout.widget.ConstraintLayout>
```

``` java
// In MainActivity.java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    // Whole widget clicked
    public void widgetClicked(View v) {
        Log.d("DEBUG-C", "widget clicked");
    }
}
```

---

## How to create a circle button (I)
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

---

## Get attribute from layout xml file
``` java
String attrValue = attributeSet.getAttributeValue("http://schemas.android.com/apk/res-auto", "attributeName");
```

```getAttributeValue()``` method returns the value of the specified attribute as a string representation.

First argument is the namespace of that attribute (type is String), second argument is the attribute name (type is String).

---

## How to create custom attributes in xml layout file
1. Create a attrs.xml inside values folder.
   ``` xml
    <?xml version="1.0" encoding="utf-8"?>
    <resources>
        <declare-styleable name="CustomButtonWidget">
            <attr name="describeText" format="reference|string" />
            <attr name="index" format="reference|string"/>
        </declare-styleable>
    </resources>
   ```
   ```declare-styleable``` tag state which class is linking to.
2. Add namespace to the top of the layout tag
   In this case, I created a namespace called "myview"
   ``` xml
    <androidx.constraintlayout.widget.ConstraintLayout
        xmlns:myview="http://schemas.android.com/apk/res-auto">

        <com.example.custommenu.CustomButtonWidget
            android:layout_width="wrap_content"
            android:layout_height="match_parent"
            android:layout_gravity="center_horizontal"
            android:layout_marginLeft="10dp"
            android:layout_marginRight="10dp"
            myview:describeText="Radio Panel"
            myview:index="0" />

    </androidx.constraintlayout.widget.ConstraintLayout>
   ```
    Then, we can use ```describeText``` attribute and ```index``` attribute these we just created inside attrs.xml file.

    To get attritube from this layout xml file, we can use ```attributeSet.getAttributeValue(String namespace, String attribute)``` method.
    ``` java
    String index = attributeSet.getAttributeValue("http://schemas.android.com/apk/res-auto", "index")  // This will return a String
    ```