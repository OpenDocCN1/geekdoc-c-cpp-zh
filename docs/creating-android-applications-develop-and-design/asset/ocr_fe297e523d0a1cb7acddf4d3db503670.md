While building a main menu is great and all, there are much more complicated uses to which you can put the Adapter and ListView combination. In fact, I'm going to show you an example that gets complicated in two ways. First, the data source is going to be from a remote URL (a Twitter feed). Second, I'm going to add a second text view to the list (you could, if you want to, add any number of items to it).

# ### THE 1000-FOOT VIEW

All right, here's the game plan. First, you'll need an AsyncTask to retrieve the feed from Twitter's API. Once you have the data, you'll need to parse it into JSON (JavaScript Object Notation) objects and feed that data into a custom adapter. Last, you'll need to create that custom adapter and the specific ListView layout to hold the two pieces of text info. With those things in hand, you can create the custom layout object.

In the end, you'll have a list of Peachpit's 20 most recent Twitter messages, along with when they were written. If a message was retweeted, the text will display in red. This is by no means the most complex list you could build using these tools, but it is a great way to show you how to make your own complex custom list views.

# ### CREATING THE MAIN LAYOUT VIEW

This step is very similar to the "Defining a Layout for Your ListActivity" section. You'll need an XML layout containing a ListView with the android:id/list ID. In this case, however, because the data isn't available when the activity launches, you'll need the ListView to start out hidden. Here's what my project's XML layout looks like:

```
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/
    res/android"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <TextView
    android:id="@+id/loading_text"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
```
```