That’s all the code you need. Time to compile it and turn it into a delegate that you can call:

```
var func = expr.Compile();
converter = func;
```

That is complicated, and it’s not the easiest to write. You’ll often find compiler-like errors at runtime until you get the expressions built correctly. It’s also clearly not the best way to approach simple problems. But even so, the Expression APIs are much simpler than their predecessors in the Reflection APIs. That’s when you should use the Expression APIs: When you think you want to use reflection, try to solve the problem using the Expression APIs instead.

The Expression APIs can be used in two very different ways: You can create methods that take expressions as parameters, which enables you to parse those expressions and create code based on the concepts behind the expressions that were called. Also, the Expression APIs enable you to create code at runtime. You can create classes that write code, and then execute the code they’ve written. It’s a very powerful way to solve some of the more difficult general purpose problems you’ll encounter.

# Item 43: Use Expressions to Transform Late Binding into Early Binding

Late binding APIs use the symbol text to do their work. Compiled APIs do not need that information, because the compiler has already resolved symbol references. The Expression API enables you to bridge both worlds. Expression objects contain a form of abstract symbol tree that represents the algorithms you want to execute. You can use the Expression API to execute that code. You can also examine all the symbols, including the names of variables, methods, and properties. You can use the Expression APIs to create strongly typed compiled methods that interact with portions of the system that rely on late binding, and use the names of properties or other symbols.

One of the most common examples of a late binding API is the property notification interfaces used by Silverlight and WPF. Both Silverlight and WPF were designed to respond to bound properties changing so that user interface elements can respond when data elements change underneath the user interface. Of course, there is no magic; there is only code that you