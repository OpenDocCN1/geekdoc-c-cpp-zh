# CHAPTER 8

# Advanced Method Concepts

| In Main x is 4 |
| In method, x is 777 |
| In Main x is 4 |

but modifications to them do not come "out." In the program in Figure 8-1, it makes no difference whether you use the name x as the Main() method's actual parameter or use some other name. In either case, the parameter received by the DisplayValueParameter\(\) method occupies a separate memory location. Figure 8-2 shows the output of the program in Figure 8-1.

# Figure 8-2 Output of the ParameterDemol program

310

![](bbox=[0.175, 0.259, 0.878, 0.542])

# Passing Parameters by Reference

On occasion, you might want to be able to alter a value you pass to it. In this case, you can pass a reference to a value. When you use a reference parameter, output parameter, or parameter array, you pass a memory address to a method, allowing the method to alter the original variable. Reference parameters, output parameters, and parameter arrays differ as follows:

+   - When you declare a reference parameter in a method header, the argument used to call the method must have been assigned a value.
- When you declare an output parameter, the argument used in the call need not contain an original, assigned value. However, an output parameter must be assigned a value before the method ends.
- When you declare a parameter array, the argument used in the call need not contain any original, assigned values, and the parameter array not be assigned any values within the method.

Reference parameters, output parameters, and parameter arrays do not occupy their own memory locations. Rather, they act as aliases, or pseudonyms (other names), for the same memory location occupied by the values passed. To use the keyword ref as

Copyright 2018 Cengage Learning. All Rights Reserved. May not be copied, scanned, or duplicated, in whole or in part. WCN 02-200-202-