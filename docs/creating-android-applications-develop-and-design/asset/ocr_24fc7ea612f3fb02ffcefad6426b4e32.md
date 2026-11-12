these side effects while trying to use an AbsoluteLayout. They'll likely try to talk you out of this lunacy.

The AbsoluteLayout, as you might have guessed, allows you to specify exactly where on the screen you want a particular view to go. Each child of an AbsoluteLayout should have android:layout_x and android:layout_y values along with the required width and height settings.

You are probably thinking, "That sounds like a great way to make layouts look exactly the way I want them to. Why bother learning anything else when I can take my screen designs and convert them directly into pixel x/y locations?"

I thought the same thing...at first.

Here's what the AbsoluteLayout layout XML looks like:

```
```xml
<?xml version="1.0" encoding="utf-8"?>

<AbsoluteLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <Button
        android:id="@+id/prev"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_x="0dp"
        android:layout_y="0dp"
        android:text="@string/prev_string"
        android:lines="1"
        android:padding="12dp"
        />
    <TextView
        android:id="@+id/url_view"
        android:layout_width="wrap_content"
```
```