When displaying error messages, in addition to telling what is wrong, the message should also tell what the user should do to solve the problem.

Use a *for* statement for counter-controlled loops. The counting variable can be declared and incremented as part of the loop structure.

# ## RESOURCES

Additional sites you might want to explore:

+   - Loops—C# Tutorial at
+     http://csharp.net-tutorials.com/basics/loops/
+   - C# Station Tutorial—Control Statements—Loops at
+     http://www.csharp-station.com/Tutorials/Lesson04.aspx
+   - C# and Loops at
+     http://www.homeandlearn.co.uk/csharp/csharp_s3p5.html
+   - Dot Net Pearls—C# and Loops at
+     http://dotnetperls.com/loops

# ## QUICK REVIEW

+   1. The three programming constructs found in most programming languages are simple sequence, selection, and iteration.
+   2. Based on a predetermined condition, iteration enables you to identify and block together one or more statements to be repeated.
+   3. The looping structures available in C# include *while*, *do...while*, *for*, and *foreach* statements. The *do...while* loop is a posttest. The others are pretest loop structures. With pretest, the conditional expression is tested before any of the statements in the body of the loop are performed.
+   4. When you know the number of times the statements must be executed, you can use a counter-controlled loop.
+   5. An infinite loop does not have provisions for normal termination. Infinite loops occur when the loop's conditional expression never evaluates to *false* or there is some inherent characteristic or problem with the loop.
+   6. With counter-controlled loops, it is important to think through test cases and check endpoints to ensure they have been used to avoid off-by-one errors.
+   7. Sentinel-controlled loops are also referred to as indefinite loops. They are useful when the number of repetitions is not known before the loop's execution. For interactive input, a sentinel value is selected and the user is told to input that value to stop. The sentinel value should not be processed.