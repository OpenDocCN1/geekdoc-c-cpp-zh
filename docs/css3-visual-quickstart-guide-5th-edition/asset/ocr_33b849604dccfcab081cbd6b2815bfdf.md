# TABLE 8.5 List-Style Values

| | <list-style-type> | IE4, FF1, S1, O3.5, CSS1 |
| <list-style-position> | IE4, FF1, S1, O3.5, CSS1 |
| <list-style-image> | IE4, FF1, S1, O3.5, CSS1 |

# Setting Multiple List Styles

You can use one line of code to set all list properties described in the previous three sections using the list-style shorthand which sets the list-style-type, list-style-position, and line-style-image properties.

Code 8.5 list-table: The list-style property lets you set the type, image, and position in all definition

To define multiple list-style attributes:

+   1. Add the list-style property to your CSS rules. Type-style, followed by a colon: (Code 8.5).

> *** CSS3 VQS | Chapter 8 | 
*** list-style-properties.css ***

```
ul {
  list-style: circle url(../images/bullet-01.
  png);
}

nav.global ul {
  list-style: none;
}
```

+   list-style:

+   2. Specify the location of your bullet image (optional). Next, a list-style-image.

```
url(arrow_02.png)
```

To include your own bullet, you must create the bullet graph and tell the browser where the image is located using either the complete Web address or the relative path of the image. (See "Creating Your Bullets" in this chapter for more information.)

![](bbox=[0.027, 0.473, 0.466, 0.653])

+   3. Specify the type. A list-style-type value from Table 8.3, followed by a space, or type none if you don't want a marker to appear.

> Code 8.5 applied to code 8.1: This version is identical to the previous version, only the code is different.

You do not need to include all of the values to ensure this shorthand selector works with. Omitted values are set to the default. The following example works fine:

circle

```
list-style:
```

+   4. Specify the position. Type a list-style-position value from Table 8.4.

If visitors have turned off graphics in their browsers or a graphical bullet does not load for some reason, the browser uses the list-type you defined in steps

List and Table Properties 219