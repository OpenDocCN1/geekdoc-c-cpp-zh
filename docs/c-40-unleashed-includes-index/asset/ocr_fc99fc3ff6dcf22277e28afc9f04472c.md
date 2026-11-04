```
Expression.Loop(
 // {
    Expression.Block(
        // if
        Expression.IfThen(
            // (i == 10)
            Expression.Equal(i, Expression.Constant(10)),
            // break;
            Expression.Goto(brk)
        ),
        // Console.WriteLine(i);
        Expression.Call(
            typeof(Console).GetMethod("WriteLine", new[] { typeof(int) }),
            i
        ),
        // i++;
        Expression.PostIncrementAssign(i)
    ),
    brk
    // }
  )
);
var f = a.Compile();
f(); // Prints 0 to 9
```

Although all of this is quite beautiful if you need to generate code dynamically at runtime, you might wonder about debugging support. There are two answers to this. First, the factory methods will raise an exception for all semantic errors they can find, making sure your trees are well formed. Second, a new debugger visualizer has been added to .NET 4 and Visual Studio 2010 to help inspect how the expression tree looks in a more comprehensible form. This proves particularly useful if you have a bunch of code that stitches together a bigger tree. Figure 21.22 shows where the icon to open the visualizer shows up when you hover over an expression tree object.

![](bbox=[0.06, 0.65, 0.83, 0.76])

Figure 21.23 shows the visualization provided by this tool, showing a textual block-based representation of the expression tree. From this, you can see many things. First, all nodes clearly have a type; even the else branch of the If (which we never stated explicitly) has