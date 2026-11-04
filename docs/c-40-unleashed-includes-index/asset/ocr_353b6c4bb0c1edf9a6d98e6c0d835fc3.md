To answer this accurately, let's first take a step back. Because we know that events are nothing but multicast delegates in disguise, we can use a plain multicast delegate as a petri dish for some experimentation. Take a look at the following fragment of code, where we use handy lambda expression syntax to make things concise:

```
Action evt = null;
evt += () => Console.WriteLine("Hello");
if (evt != null)
    evt();
evt -= () => Console.WriteLine("Hello");
if (evt != null)
    evt();
```

Pop quiz: How many times does it print Hello? If you say once, think twice; the answer is two times. Although it looks like we're adding and removing the same event handler on lines two and four, those are not the same object. Recall what anonymous functions compile into under the hood: compiler-generated methods containing the code specified in the anonymous function expression:

```
Action evt = null;
evt += new Action(__AnonymousMethod1);
if (evt != null)
    evt();
evt -= new Action(__AnonymousMethod2);
if (evt != null)
    evt();
```

Two anonymous function expressions result in two distinct methods being cooked up by the compiler, even though they have the same code inside them. The compiler could be smarter about this, detecting “semantically identical” anonymous function expressions and sharing the same object for them. However, this is a pretty tricky thing to implement, and the compiler writers thought there were more important matters to tackle.

Because we have two distinct methods used when adding and removing delegates, the += and -= operations do not cancel each other out. The way to fix this issue is to use an intermediate variable:

```
Action evt = null;
Action handler = () => Console.WriteLine("Hello");
evt += handler;
if (evt != null)
    evt();
evt -= handler;
if (evt != null)
    evt();
```