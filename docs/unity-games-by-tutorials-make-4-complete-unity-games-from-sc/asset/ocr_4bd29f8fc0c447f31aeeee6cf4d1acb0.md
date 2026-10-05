# [RequireComponent (typeof (Text))]

This line of code enforces that a Text component must be available. Unity will automatically add the component, and it will prevent you from removing it so long as the attribute is there.

# SerializeFieldField

You can use this attribute when you want a field to be accessible in the Inspector, but not accessible from other scripts.

```
[SerializeField]
private bool isAlive = true;
```

Using the above code, you can now set the value of isAlive in the Inspector, but not from other scripts.

# HideInInspector

You can also hide public values in the Inspector as well.

```
[HideInInspector]
public int Score
```

Here, the variable is exposed to other scripts but will not appear in the Inspector.

# Setting a range

Instead of using a text field to set a number, you can use a slider instead. This means that a value will never be outside any range.

```
[Range (1,100)]
public int secretNumber;
```

The field will now look like this in the Inspector:

![](bbox=[0.118, 0.706, 0.875, 0.735])

# Special folders

Throughout the book, you've organized the Project browser according to the assets used. Placing assets in these folders alters the behavior of the editor. Typically, you do to tweak the editor to your needs, but you can also create a plugin for the editor as well.