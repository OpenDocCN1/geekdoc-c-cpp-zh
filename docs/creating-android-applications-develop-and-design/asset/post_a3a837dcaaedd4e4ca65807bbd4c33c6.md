
## CREATING A LISTACTIVITY

Now you need a place to display your items. You'll create an instance of ListActivity in which to display your recently created list.

Every screen must have an activity, and list screens are no exception. In this case, Android provides you a helper class that was built specifically to make list screens easier. It's called the ListActivity, and it behaves exactly like an activity does except that it has a few extra methods to make life easier. If you're coding along with the chapter, you'll need to create a new project. Take the main activity you'd normally have, and modify it to look like the following listing:

```
package com.haseman.lists;

import android.app.ListActivity;
import android.os.Bundle;

public class MainMenuActivity extends ListActivity{
	public void onCreate(Bundle bundle){
		super.onCreate(bundle);
		setContentView(R.layout.list_activity);
	}
}
```

This code will not, however, compile at the moment, because I haven't yet defined what R.layout.list_activity looks like. Guess what you're going to do next?

## DEFINING A LAYOUT FOR YOUR LISTACTIVITY

You will need to create an XML layout file for your list. Again, this is similar to other layout tasks you've done, with one notable exception: You need to define a ListView with the special ID android:id/list. This is what tells the system which list view is the main list view your new ListActivity will interact with. I've also added a TextView to the layout as a large title. My XML file looks like the following:

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">
        <TextView
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1"
        android:text="@string/main_menu"
        android:gravity="center"
        android:textSize="40dp"/>
    <ListView
        android:id="@android:id/list"
        android:layout_width="fill_parent"
        android:layout_height="0dp"
        android:layout_weight="1"
    android:gravity="center"/>
</LinearLayout>
```

> **TIP:** Special IDs: You only need to call the android:id/list ListView if you're using the built-in convenience methods of ListActivity. If you're using a regular activity, you can use any ID you want. This special ID is what connects the ListActivity to the single ListView with which it is going to interact.

### AN OPTIMIZATION TRICK

When you're depending on a LinearLayout to portion up all available space for your views, you can save a tiny bit of time by specifying that the dimension (in the child layout) be 0. This means the system doesn't have to figure out the ideal size of the object when it walks through your layout to measure your views before drawing. This may not help a lot, but if you've got a layout with a lot of views, every little bit counts. As you can see in the previous code listing, I've specified the heights be 0 because the LinearLayout is going to parcel out all the space between them. You'll also need to specify a weight for the view, or it might not work.

This XML layout code should look familiar to you, given what you've read in previous chapters. It's simply splitting the screen space between the title main menu and the list of sub-screens. You can also see the special Android list ID that is needed to tell the ListActivity which view it should interact with.

### MAKING A MENU LIST ITEM

Now you'll create a layout XML file for the individual list element.

You'll need to declare a separate layout object to define how each element will look in the list. I'm using a very simple version of the ArrayAdapter, so at this point, the layout XML file *must* contain only a single text view. We'll get into more-complex menu items later in the chapter.

Next, you'll need to create a new file, containing a single text view, in the /res/layout/ folder. Here's what /res/layout/list_element.xml looks like in my project:

```xml
<?xml version="1.0" encoding="utf-8"?>
<TextView
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:gravity="center"
    android:layout_height="wrap_content"
    android:layout_width="match_parent"
    android:textSize="20dp"
    android:padding="15dp"/>
```

You don't actually need to supply an ID for this text view, because you'll be referencing it in its capacity as a layout object (R.layout.list_element, in this case). Setting the gravity to center tells the view that you want the text to lie in the center of the extra available space. Setting the padding to 15dp will also give the views a little bit of extra space, so people with hands like mine can hit the correct one.

Now that I've declared what I want the list elements to look like, I can go about adding them to the ListView itself.

### CREATING AND POPULATING THE ARRAYADAPTER

Create and configure an ArrayAdapter. The ArrayAdapter will communicate your data to the ListView. It will also inflate however many copies of the list_element layout are needed to keep the ListView full of data. As a last step, here's what you'll need to add to the MainMenuActivity's onCreate method:

```java
public void onCreate(Bundle bundle){
    super.onCreate(bundle);
    setContentView(R.layout.list_activity);
    ArrayAdapter<CharSequence> adapter =
        ArrayAdapter.createFromResource(getApplicationContext(),
        R.array.menu_entries, R.layout.list_element);
    setListAdapter(adapter);
}
```

Because the ListView has the special @android:id/list system ID, the List Activity knows where to find the ListView. As a result, you'll only have to create the adapter and hand it over to the ListActivity. The ListActivity will make sure that it's correctly plugged into the ListView and that everything is drawn correctly.

**FIGURE 5.1** A very basic main menu.

![](img/47ad0ac10bf11125744ef22c945d3099_147_0.png)

To create the ArrayAdapter, I specify the array of strings I defined in the section "Creating the Menu Data" as well as the `list_element` layout I created in "Making a Menu List Item." Assuming that all your Tab A's are correctly fitted into your Slot B's, the resulting screen will look something like Figure 5.1.

Do a little dance—you've now got a functional (albeit very simple) list! Have a smoke, cup of coffee, sip of wine, or dog treat. Whatever you do to reward yourself for a job well done, do it now. I'll be here when you get back.

## REACTING TO CLICK EVENTS

Your code will need to listen for item clicks.

What's the point of having a menu if you can't tell when items have been selected? Right, there isn't one. Let me show you the final piece to my basic list menu example. Add the following method to your MainMenuActivity.java file:

```java
@Override
public void onListItemClick(ListView lv,
        View clickedView,
        int position, long id)
{
    super.onListItemClick(lv, clickedView, position, id);
    TextView tv = (TextView)clickedView;
    Toast.makeText(getApplicationContext(),
        "List Item "+tv.getText()+" was clicked!",
        Toast.LENGTH_SHORT).show();
}
```

The ListActivity will call this method (if you've defined it) every time an element in the list view is clicked (or tapped with a finger). For more-complicated lists, you may want to use the ID (especially if you are using SQLite as a backing store). For this simple demo, I've just popped up a little dialog showing the text of the item that was pressed. If you're implementing your own basic main menu, I suggest you use the position of the clicked item to start an activity, service, or other action. You can see an example of this if you look at the associated source code.

That's the most basic list view I could possibly show you. Now, I'll take you in the opposite direction and show you what a custom list backed by a remote data source looks like.
