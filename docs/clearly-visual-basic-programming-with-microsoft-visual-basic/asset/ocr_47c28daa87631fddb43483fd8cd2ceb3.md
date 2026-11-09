```
‘clear label controls
lblOriginal.Text = String.Empty
lblAscending.Text = String.Empty
lblDescending.Text = String.Empty
```

Next, you will display the contents of the array in the lblOriginal control. You can accomplish this task using a loop to access each element in the array, beginning with the element whose subscript is 0 and ending with the element whose subscript is 3. Because you want the loop instructions processed a precise number of times—in this case, from 0 to 3—you will code the loop using the For...Next statement. As you learned in Chapter 15, the For...Next statement provides a more convenient way to code a counter loop because, in addition to evaluating the loop condition, it also handles initializing and updating the counter variable. Figure 19-4 shows two versions of the appropriate code. Only the endValue in the For clause is different in each version. In Version 1, the endValue is 3 (the highest subscript in the array). In Version 2, the endValue is the expression strFriends.Length - 1. The expression uses the array’s Length property, which contains an integer that represents the number of elements in the array; in this case, the Length property contains the number 4. To determine the highest subscript in the array, you simply subtract the number 1, as shown in the expression. Although both versions of code in Figure 19-4 will work, Version 2’s code is the preferred one for several reasons. First, if you use the Length property, you won’t have to count the number of array elements yourself. Second, the Length property is essential when you don’t know the exact number of array elements; this may be the case when the array values come from a file. Finally, if the number of array elements changes in the future, the Length property’s value will automatically adjust.

![](bbox=[0.052, 0.632, 0.785, 0.859])

**Figure 19-4:** Two versions of the For…Next statement