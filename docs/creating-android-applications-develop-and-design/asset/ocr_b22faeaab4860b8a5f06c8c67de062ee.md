Here is the first of the child views in the definition for the Prev button:

```
```xml
<Button
    android:id="@+id/prev"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:paddingLeft="5dip"
    android:paddingRight="5dip"
    android:text="@string/prev_string"
    android:lines="1"
    android:layout_weight="1"
/>
```
```

The layout_weight value, which can be any decimal number from 0 to 1, tells the system how much space to give to the child view when the layout has either too much or too little space.
Take a look at the landscape version of the button bar again (Figure 3.6).

FIGURE 3.6 Overly large buttons thanks to the LinearLayout.

# LINEAR LAYOUTS ARE NOT FOR PIXEL PERFECTIONISTS

I've said it once and I'll now say it a second time: LinearLayouts are not great for laying out pixel-perfect screens. As views get proportionally larger and smaller, it becomes difficult to get them to rest exactly where you want them to. Use the LinearLayout when you have a known quantity of objects that must get on the screen and you're not overly picky about exactly where they end up. In small, space-constrained cases, as with small button bars or single list menu entries, AbsoluteLayouts can prove to be much easier to use to get exactly the screen layout you're looking for. This might be the only case I can think of where an AbsoluteLayout might make sense.