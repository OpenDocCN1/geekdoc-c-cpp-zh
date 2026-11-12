
## SPECIAL DIMENSIONS

You are always required to give a height and width for every view in your hierarchy. You may use, for these definitions in particular, four different values. They are:

- `wrap_content` makes the view big enough to match what it contains. This might mean different things to different views, but the concept remains the same.
- `fill_parent` and `match_parent` values actually mean exactly the same thing. Namely, I want the dimensions of this view to match the dimensions of my parent view.
- `dip` or `dp` stands for device-independent pixels. This is a value that will give you a consistent spacing regardless of the screen density (pixels per inch) of the device. On the Nexus 1 or Nexus S, 1 dp ~= 1.5 pixels.
- `px` stands for pixels. There are times when exact pixel values are necessary. I advise against using this to declare screen locations, but it's an option.

Let's look at what is happening in the java code. Instead of calling setContentView on an ID from the R.java file, I'm passing it an instance that the LinearLayout object returned from the buildLayouts method. In the buildLayouts method, I'm first creating a new LinearLayout (passing in the application's context) and a new LayoutParams object. To match what's in the XML, the new LayoutParams is initialized with both the width and the height set to MATCH_PARENT. If you have done Android development before, you should know that MATCH_PARENT is exactly the same as the previously used FILL_PARENT.

Once I have the layout parameters initialized for the top LinearLayout, I can pass them to the object with a setLayoutParams call. I've now got the LinearLayout configured, so it's time to move on to building the TextView.

This is a simple text view, so its layout parameters are very similar to those of its parent's layout. The only noticeable difference is that I'm setting the height, when creating the layout parameters, to scale to fit the natural size of the TextView. (Much more on dynamic heights and widths soon.)

Once I've told the TextView how it will be positioned in its parent layout via the layout parameters, I tell it which string I'd like to display. This string is defined in /res/values/strings.xml. The name attribute in XML determines what needs to appear after R.string for the system to locate your resource. You'll learn much more about resource management in the next section.

Last, I need to add the new TextView into the LinearLayout and then return the LinearLayout so it can be set as the main content view for the activity. Once that's finished, I have a layout constructed at runtime with Java code, which identically matches the layout provided by the system in XML form.

The Java code looks fairly straightforward, but XML is a much better idea for working with the layout. Using XML, you can use Android's resource management system and give non-software engineers the ability to modify the application UI.

## ALTERING THE UI AT RUNTIME

It's one thing to use XML or Java to define the pile of views that compose your user interface. But particularly in the XML case, you'll want to be able to retrieve and alter views with data acquired over the network, from the user, or from any other information source. Android provides a simple method for gaining access to the views that currently compose your screens by calling findViewById, which is an Activity class method.

### IDENTIFYING YOUR VIEWS

Before you can find one of your views at runtime, you'll need to give it an ID. Once you've called setContentView on an activity, you can call findViewById to retrieve your views and then alter them. This process should look at least a little bit familiar, because you saw it in the previous chapter. Here's what it looks like in XML:

```xml
<TextView
    android:id="@+id/text_holder"
    android:layout_width="fill_parent"
    android:layout_height="wrap_content"
    android:text="@string/hello"
    />
```

In this case, I've added an android:id line to name the TextView. The @+ notation tells Android that rather than referring to a view, you'd like to create an ID for the view. The first reference to any ID must start with @+id. Subsequent references to that ID will start simply with @id.

Android keeps its own reserved IDs namespace. For example, if you're creating a layout to be used by ListActivity (an activity specifically designed to show lists of information), you'll want to set the ID on your main onscreen ListView to `android:id="@id/android:list"`. These well-known IDs allow Android's system code to correctly find and interact with the list view that you specify. I'll provide you with more on this subject in Chapter 5, which covers list creation and management.

If you're creating a view at runtime, simply call setId and pass in an integer, and you'll be able to retrieve it later.

### FINDING YOUR RESOURCES WITH ANDROID

When Android compiles your project, it assigns a number value for your new static numeric ID. It places this new ID in the R.java file within your project. This file is your gateway to everything you've defined inside the res folder. For every layout, drawable, and identified view—and for a host of other things—Android places a subsequent statically defined int into the R file that identifies those things. Anytime you add a line to your layout XML defining a new ID (for example, android:id="@+id/my_new_id"), you'll find that after the next time you compile your project, you'll have an entry in the R.id class. In the previous example, this entry would be R.id.my_new_id.

### RETRIEVING A VIEW

Getting the existing instance of an Android view is as simple as calling findViewById and passing in the ID value found in the R.java file. Given the earlier XML example, here's how you would grab an instance of the text view and modify its contents.

```java
public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.main);
    TextView tv = (TextView)findViewById(R.id.text_holder);
    if(tv!=null)
        tv.setText(R.string.hello);
}
```

## HANDLING A FEW COMMON TASKS

Some tasks are more common than others. Let's take a look at how you can handle some of the ones that you'll do a few dozen times before you finish your first application.

![](img/47ad0ac10bf11125744ef22c945d3099_76_0.png)

### CHANGING THE VISIBILITY OF A VIEW

Most of the time, if you want to define your UI in XML, you'll need to add views that will be visible only some of the time.

> **TIP:** If you find yourself doing this a lot, be sure to check out the ViewStub class.

Depending on how dynamic your application is, views come and go fairly regularly. Showing and hiding views is as simple as using the ever trusty findViewById and then calling setVisibility on the returned object:

```java
Button button = (Button)findViewById(R.id.sample_button);
//Cycle through the View Visibility settings
if(button != null){
    //Gone (no impact on layouts)
    button.setVisibility(View.GONE);
    //Invisible (holds its space in a layout but is not drawn)
    button.setVisibility(View.INVISIBLE);
    //Visible (duh)
    button.setVisibility(View.VISIBLE);
}
```

This code has three visibility settings. GONE and VISIBLE are the most obvious. You'll find yourself using INVISIBLE less often, however, it's great for keeping all the other views inside your layouts from moving around when you want to hide something.

### SETTING AN ONCLICKLISTENER

Setting up a listener to tell you that one of your views has been clicked is one of the most common tasks you'll do when working on an Android application. A click can mean the user moved focus to your view using the navigation pad or trackball and then clicked the select key. A click can also mean pressing on the trackball, if there's one of those, or on the key in the center of the four- or eight-way directional pad.

Your click listener will also be called if, in touch mode, the user taps their finger down on your view and then lifts up with their finger still within the bounds of the view. This is an important distinction, as your click listener will not be invoked when their finger actually clicks down on the view but rather when the user lifts their finger up. This gives the user the chance to put a finger down in the wrong place and then correct the position before lifting it.

You can track view clicks in several ways. You can declare that your activity itself implements the view's OnClickListener interface, add a `public void onClick(View v)` method, and pass a pointer to your activity to the view you wish to track. Here's what that looks like in code for theoretical buttons with IDs button_one and button_two declared in an imaginary main.xml layout file:

```java
public class UiDemoActivity extends Activity implements
        OnClickListener {

    @Override
    public void onClick(View selectedView) {
        if(selectedView.getId() == R.id.button_one){
            //Take Button One actions
        }

        if(selectedView.getId() == R.id.button_two){
            //Take Button Two actions
        }
    }

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);
```
