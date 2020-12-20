## Android.widget.Toast Class Information
### Public Methods (official doc: https://developer.android.com/reference/android/widget/Toast)
#### makeText
Make a standard toast that just contains text from a resource.

***public static Toast makeText (Context context, int resId, int duration)***

**Parameters**

*Content*:

Type: Context.

Info: Which object

*resId*:

Type: int.

Info: The resource id of the string resource to use. This is from string.xml file.

*duration*:

Type: int.

Info: How long to display the message.

***public static Toast makeText (Context context, CharSequence text, int duration)***

**Parameters**

*Content*:

Type: Context.

Info: Which object

*text*:

Type: CharSequence.

Info: The text to show.

*duration*:

Type: int.

Info: How long to display the message.

``` java
Toast.makeText(this, "Alert, something not right!!!", Toast.LENGTH_LONG).show();
```
