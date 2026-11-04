From this perspective, the essence of the DLR is to provide tree-stitching services for
expression tree fragments that are handed to it through language-specific binders. This
also explains why the expression tree API was enhanced to support statement tree nodes—
because call sites like those need conditional logic.

# ## EXPRESSION TREES AS A NEW SWISS KNIFE

The use of expression trees is becoming more and more apparent with every release of
the .NET Framework. Initially meant as a way for LINQ providers to make sense of user
intent, they now act as the common back end of all sorts of compilation tasks at run-
time. Languages such as IronPython and IronRuby always turn code into expression
trees to execute the code efficiently through IL.

Figure 22.16 shows the states the Target delegate code behind our call site is going
through upon invocation using different combinations of argument types. It’s left as an
exercise to draw the corresponding expression/statement trees that are used to represent
this code before the dynamic language runtime compiles it.

![](bbox=[0.093, 0.337, 0.885, 0.83])

FIGURE 22.16 A call site getting updated upon feeding in new input types.

The call site for the WriteLine call works in a similar way. In this case, the first argument
is statically determined as typeof(Console) because we specified this in the original C#