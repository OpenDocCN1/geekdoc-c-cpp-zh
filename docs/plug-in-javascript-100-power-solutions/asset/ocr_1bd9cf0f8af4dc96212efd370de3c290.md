# Chapter 3: The Core plug-ins

This statement will assign the value "The product of 6 and 7 is 42" to string. All you have to remember is to use the same number of tags as there are values to be inserted.

# The Plug-in

```
function InsVars()
{
  var tmp = arguments[0]

  for (var j = 1; j < arguments.length; ++j)
    tmp = tmp.replace(new RegExp('#' + j, 'g'), arguments[j])
  return tmp
}
```

# StrRepeat()

Unlike other languages, JavaScript doesn't come with a function to create a new repeated string. So there's a plug-in to do the job, as shown in Figure 3-16, in which a cheer is repeated three times.

# About the Plug-in

This plug-in creates a repeated string based on a string and a number. It takes these

+   * str A string to repeat
* num The number of times to repeat the string

# Variables, Arrays, and Functions

| tmp | Local string variable used to store the string as it is assembled |
| j | Local integer variable used for looping |

**Figure 3-16** Plug-in JavaScript - Message from webpage
Using this plug-in to create a cheer.

![](bbox=[0.295, 0.708, 0.842, 0.901])