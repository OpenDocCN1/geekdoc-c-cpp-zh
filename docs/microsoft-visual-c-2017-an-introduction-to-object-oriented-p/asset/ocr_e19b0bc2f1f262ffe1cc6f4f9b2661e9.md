# Returning a Reference from a Method

invalid element that uses a negative subscript (–1) is returned from the method. You need to learn about exception handling in Chapter 11 before you can handle this mistake.

In the Main() method, following the call to FindItem(), item, which represents the memory address of the matching element, is set to 0 to indicate that it is no longer available. When the items array is displayed, the correct element has been changed to 0. Figure 8-15 shows two separate executions of the program in which a different items element is removed each time.

```
Before replacement:
123 241 375 410 555
Enter the value to find >> 410
After replacement:
123 241 375 0 555
```

```
Before replacement:
123 241 375 410 555
Enter the value to find >> 123
After replacement:
0 241 375 410 555
```

**Figure 8-15** Two typical executions of the Returns of ReturnRefDemo program

You could accomplish the removal of the items array in the ReturnRefDemo program without returning a reference. For example, you could create the FindItem() method to return an integer subscript that is not a reference and use it to access the desired element in the Main() method. So, for now, returning a reference from a method will be of limited value to you. However, you should understand that you can return a reference in C#, and you might someday use the technique in a large program where it might be impractical to pass large amounts of data into and out of methods and much more practical to pass references.

# TWO TRUTHS & A LIE

# Returning a Reference from a Method

+   1. A reference can be returned from any method.
2. When a reference is returned from a method, the calling method receives a new address.
3. When a method returns a reference, it cannot also return a value.

> For example, you can return a reference from a method if the value was passed into the method. The false statement is: #. There are some restrictions on the uses of ref returns.

Copyright 2018 Cengage Learning. All Rights Reserved. May not be copied, scanned, distributed, or in in part. WCN 02-200-219 **