enumeration value with cases for every possible enumeration value, a code snippet can be used (see Figure 7.7).

# 1. IntelliSense for Switch Snippet

![](bbox=[0.07, 0.26, 0.48, 0.38])

# 2. Press Tab Twice and Type Color

![](bbox=[0.07, 0.47, 0.48, 0.6])

# 3. Press Enter

![](bbox=[0.07, 0.69, 0.42, 0.85])

FIGURE 7.7 Code snippet for switch on enumeration value.

# A "COMPLETE" SWITCH

Enumerations denote a finite set of known constant values that belong to the same domain. For example, we've defined three colors, and that's it. So in essence, the switch illustrated here is "complete" because it stretches the whole range of possible values. Or is it?

First, why would we bother about a switch having the property of being complete? Here's why: Suppose you want to write a function that returns some value for every potential case, as shown here:

```
string ToDutchString(Color color)
{
    switch (color)
    {
        case Color.Red:
            return "rood";
```