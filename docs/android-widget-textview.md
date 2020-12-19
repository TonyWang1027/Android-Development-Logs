## Android.widget.TextView Class Information
### Public Methods (official doc: https://developer.android.com/reference/android/widget/TextView)
#### setText

*public final void setText (int resid)*
This allows you to pass a int value into setText method

``` xml
<resources>
    <string name="textView">Some text here!</string>
</resources>
```

``` java
TextView myTextView = findViewById(R.id.textView);
myTextView.setText(R.string.textView);
```

\
*public final void setText (CharSequence text)*
*CharSequence* is just an array of chars, it's equal to type "String".

``` java
TextView myTextView = findViewById(R.id.textView);
String tempString = "Hello";
myTextView.setText(tempString);
```
