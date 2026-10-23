![](bbox=[0.15, 0.08, 0.78, 0.35])

**FIGURE 7.2:** Simple image of memory layout for a few variables. The objects on the right side are overly simplified, especially the list, but this portrays sufficient detail for understanding what is happening at this point.

All of these have been made as vars just to give us the option of altering them below. Normally we would want to use a val unless we explicitly found a reason why we had to change them. In this case the reason is just for illustration.

The memory layout looks something like what is shown in figure 7.2. This is an idealized representation. In reality memory is all linear and has structure to it that will be discussed in chapter 13. For now, this view is sufficient. On the left are boxes that represent the variables. In Scala the best mental better picture is to see the variables as boxes that store references to values. In some situations Scala will put the actual values in the boxes for the variables, but that is an optimization that you do not really have control over and it will not alter the behavior, so it is good to picture the memory like this.

What happens to this picture if we change the value of two of the variables? For example, say that now we execute these two lines of code.

```
i1=8
s1="New string."
```

The first one changes i1 so that it references the value 8. The second one changes the s1 so that it references this alternate String. What would this look like in memory? The result is shown in figure 7.3. The 5 and the String “Scala is fun!” have not been changed. They remain in memory just like before. Because nothing references them, these objects will be collected and disposed of automatically. What has changed is the references in i1 and s1. They now point to new objects in new chunks of memory that hold these new values. Both the Int and String types are immutable. As a result, once the objects are created, nothing can change them. They do not allow any operations that would alter their values. If we had made these variables using val we would not be able to change where the arrows point either.

Indeed, all of the types used here are immutable with the exception of the Array. So Array is the only one where we can change the value in the box on the right. To see how