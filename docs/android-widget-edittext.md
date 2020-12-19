## Android.widget.EditText Class Information
### Public Methods (official doc: https://developer.android.com/reference/android/widget/EditText)
#### getText

*public Editable getText()*
It returns **android.text.Editable** type, not **String** type. Use toString() method to get the actual string.

Because, the return type Editable is implement CharSequence interface, so, it can pass into setText() method as an argument stright away.

The return value should not be modified. If you want a modifiable one, you should make your own copy first.

``` java
EditText myEditText = findViewById(R.id.editText);
String text = myEditText.getText().toString();
Log.d("Debug", "Text: " + text);   // Information about Log class, see android.util.Log class
```

``` java
EditText myEditText = findViewById(R.id.editText);
TextView myTextView = findViewById(R.id.textView);
myTextView.setText(myEditText.getText());
```
