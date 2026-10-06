# Chapter 4: Location and Dimensions 79

# 22 Position()

This plug-in sets the CSS style.position property of an object. This is useful when you want to control an object's offset from its parent's location, or even completely move it to any absolute position. Figure 4-4 shows a div that has been offset horizontally from its previous position by 100 pixels.

# About the Plug-in

This plug-in sets the CSS style.position property of an object. It requires the following arguments:

+   - id An object, an object ID, or an array of objects/or object IDs
- type The type of style.position property to assign, out of 'absolute', 'fixed', 'relative', 'static' or 'inherit'. You can also use the shorter, global variables (created by the Initialize() plug-in) of ABS, FIX, REL, STA and INH.

# Variables, Arrays, and Functions

| position | The object's style.position property |

# How It Works

This function uses the capability of the S() function that accepts an object, an object ID, or even an array of objects/or object IDs. Therefore, it simply passes the values in id and type directly to the S() plug-in.

# How To Use It

To set an object's style.position property using this plug-in, make a call such as:

```
Position('myobject', ABS)
```

![](bbox=[0.125, 0.663, 0.767, 0.846])