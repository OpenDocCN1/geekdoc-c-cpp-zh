Add the following highlighted code to the onKeyDown listener that you've dealt with before:

```
```java
public boolean onKeyDown(int keyCode, KeyEvent event){
    //...previous keycode code skipped...
    if(keyCode == KeyEvent.KEYCODE_DPAD_DOWN){
        Intent actionStartIntent= new Intent("com.haseman.PURPLE_PONY_POWER");
        actionStartIntent.putExtra("newBodyText",
            "You Pressed the Down Key!");
        startActivity(actionStartIntent);
    }
}
```
```

You're adding a string payload to the intent before using it to start an activity. Whoever receives the intent will be able to pull this string out (assuming they know it's there) and use it as they see fit. Now that you know how to attach the data, let's take a look at an example of retrieving and using the string in NewActivity's onCreate method:

```
```java
public void onCreate(Bundle icicle){
    super.onCreate(icicle);
    setContentView(R.layout.new_activity);
    Intent currentIntent = getIntent();
    if(currentIntent.hasExtra("newBodyText")){
        String newText = currentIntent.getExtras().getString("newBodyText");
        TextView bodyView = (TextView)findViewById(
            R.id.new_activity_text_view);
        bodyView.setText(newText);
    }
}
```
```