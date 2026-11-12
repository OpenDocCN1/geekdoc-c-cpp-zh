![](bbox=[0.079, 0.168, 0.379, 0.54])

![](bbox=[0.405, 0.169, 0.896, 0.397])

**FIGURE 7.1** A simple screen with two buttons.

**FIGURE 7.2** The buttons are far too large in landscape mode.

```
~~~xml
android:layout_marginLeft="30dp"
android:layout_marginRight="30dp"
android:layout_marginBottom="60dp"
android:layout_width="fill_parent"
android:layout_height="wrap_content"
android:text="@string/no_button_text"
android:layout_alignParentBottom="true"
/>
~~~
```

What you see in this code listing shouldn't be anything new, given your experience with the RelativeLayout in previous chapters. I've declared two buttons, pinned the No button to the bottom, and aligned the Yes button above it. When shown in portrait mode, these buttons look simple but pretty good (Figure 7.1).

While this will only win me a design award if the judges are partially blind, it's a fairly good-looking, simple, and functional screen. But take a look at what happens when I switch it to landscape mode (Figure 7.2).