# Chapter 4: Location and Dimensions

![](bbox=[0.222, 0.11, 0.775, 0.258])

FIGURE 4-5 The GoTo() plug-in moves an object.

# About the Plug-in

This plug-in moves an object (if it is movable) to a new location. It takes the following arguments:

+   - An object, an object ID, or an array of objects and/or object IDs
- The horizontal offset, from the left edge of the parent object, to which the object should be moved (from the browser edge if the object has a style.position property of 'fixed' or 'absolute')
- The vertical offset, from the top of the parent object, to which the object should be moved (from the browser top if the object has a style.position property of 'fixed' or 'absolute')

# Variables, Arrays, and Functions

| left | The object's style.left property |
| top | The object's style.top property |
| Px() | Plug-in to add the suffix 'px' |

# How It Works

This plug-in also takes advantage of the S() plug-in's capability to manage arrays of objects and/or object IDs, single objects, or object IDs. It makes just two calls: one to set the object's style.left property to the value in x with the suffix 'px' appended, as is required by the rules of CSS, and the other to do the same but with the style.top property using the value in y.

# How To Use It

To use this plug-in make sure that an object is movable by first issuing a command like this (using the global variable REL, which contains the string 'relative'):

```
Position('advertdiv', REL)
```