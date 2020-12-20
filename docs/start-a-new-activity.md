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
