# Chapter 41
Tips and Tricks with Subprograms

a procedure doesn’t. Of course, if you pass your arguments by reference, then both of them can return many results—indirectly, of course.

+   ➢ determine which variables participate in each part of the script and their roles in that part. The flowchart that follows can help you decide what to do with each variable, whether it should be passed to the subprogram and/or returned from the subprogram, or if it should just be a local variable within the subprogram.

![](bbox=[0.177, 0.219, 0.934, 0.799])

So, with the help of this flowchart, let’s discuss each part of the script independently! The parts that are not marked with a dashed rectangle will comprise the main code.

# First part

In the first part of the script, there are three variables: $i, $temp1, and $sex. However, not all of them must be included in the formal argument list. Let’s find out why!