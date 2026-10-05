```
Circle c = new Circle();
int i = 42;
object o;
o = c; // refers to a circle
i = o; // what is stored in i?
```

To obtain the value of the boxed copy, you must use what is known as a cast. This is an operation that checks whether converting an item of one type to another is safe before actually making the copy. You prefix the object variable with the name of the type in parentheses, as in this example:

Click here to view code image

```
int i = 42;
object o = i; // boxes
i = (int)o; // compiles okay
```

The value of this cast is subtle. The compiler notices that you've specified the type int in the case. Next, the compiler generates code to check what o refers to at runtime. It could be absolutely anything. Just because your cast says o refers to an int, doesn't mean it actually does. If o really refer to a boxed int and everything matches, the cast succeeds, and the compiler-generated code extracts the value from the boxed int and copies it to i. (In this example, the boxed value is then stored in i.) This is called unboxing. The following diagram shows what's happening:

![](bbox=[0.142, 0.626, 0.597, 0.758])

On the other hand, if o does not refer to a boxed int, there is a type mismatch, causing the cast to fail. The compiler-generated code throws an InvalidCastException exception at runtime. Here's an example of unboxing cast that fails: