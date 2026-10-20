![](bbox=[0.12, 0.11, 0.75, 0.42])

+   - Finally, we come to the assignment of the return value to v:
+     v = createAndInsert();

Here, we really get behavior that can be improved: the usual assignment operator has the goal of giving v the same value as the source value that is assigned. In general, any assigned value should not be modified and should be independent from the object that the value was assigned to. So, the assignment operator will create a deep copy of the whole return value:

![](bbox=[0.12, 0.58, 0.75, 0.89])