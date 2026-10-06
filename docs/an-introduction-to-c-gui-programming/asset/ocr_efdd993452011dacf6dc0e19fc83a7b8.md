list of property names and property values. In this case, we are setting the relief property of the GtkButton btn2 to GTK_RELIEF_NONE.
The ‘relief’ of a GtkButton controls how the border looks. The borders of some GTK widgets have a degree of shading applied around them to provide a 3D appearance - by default, a GtkButton has this shading applied, which makes the button appear to stand out slightly from the window background. By setting the relief to GTK_RELIEF_NONE, this 3D shading is removed – if you run the program above, you should be able to clearly see the difference between the two buttons on the window. (You can use the TAB key to move the dotted outline between the buttons to show the difference more clearly.)

![](bbox=[0.101, 0.319, 0.399, 0.467])

+   - A GtkButton with the relief property set to GTK_RELIEF_NONE

Here's another example. Remove the setting of the relief property and change the name of the button by adding an underscore

```
GtkWidget *btn2 = gtk_button_new_with_label ("My button");
```

You should end up with a button that looks like this:

![](bbox=[0.101, 0.626, 0.399, 0.774])

+   - A GtkButton with an underline in the label and the use-underline property set to FALSE

If you now set the use-underline property:

```
Gtk_object_set (G_OBJECT (btn2), "use-underline", TRUE, NULL);
```

the underscore will vanish, but reappear under the ‘b’ of ‘button’ if you hold down the ALT key on the keyboard.