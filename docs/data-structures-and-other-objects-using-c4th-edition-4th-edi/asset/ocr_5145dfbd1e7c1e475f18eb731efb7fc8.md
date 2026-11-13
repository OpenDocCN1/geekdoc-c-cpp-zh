```
2. while (both halves of the array have more elements to copy)
   if (data[copied1] <= (data + n1)[copied2])
   {
       temp[copied] = data[copied1] ;
       Add 1 to both copied and copied1.
   }
   else
   {
       temp[copied] = (data + n1)[copied2] ;
       Add 1 to both copied and copied2.
   }
```

In our actual implementation, the two assignment statements can be modified to also add 1 to copied and to the appropriate one of the other two local variables (copied1 or copied2). The modified assignment statements make use of the ++ operator, as shown here:

+   1. Initialize copied, copied1, and copied2 to 0.

```
2. while (both halves of the array have more elements to copy)
   if (data[copied1] <= (data + n1)[copied2])
       temp[copied++] = data[copied1++];
   else
       temp[copied++] = (data + n1)[copied2++];
```

Using an index such as copied++ has the effect of using the current value of the variable copied as the index and afterward adding 1 to the variable. (If we wanted to add 1 before using the index, we would write ++copied instead of copied++).

This part of our algorithm works fine as long as neither half of the array runs out of elements. However, eventually one of the two halves will run out of elements. For our example, this will occur after we copy the last element (20) from the second half of the data array to the temporary array, as shown here:

![](bbox=[0.175, 0.645, 0.7, 0.85])