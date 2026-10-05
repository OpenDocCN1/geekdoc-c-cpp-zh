unexpected results. Often, it's compiler error messages that you need to interpret, especially when using the standard library. Therefore, I wanted to be clear on this point about how the compiler proceeds, so you can correctly interpret the error messages.

You might now wonder what happens if the type is already const& when instantiated—as in print—you also enrich it with const& Well, the rules are quite simple:

+   - When two const meet, the result is const.
- When two &s collide, the result is &.

So if it happens that you pass the return of a_or_b into print, the compiler instantiates void print(const int&)—not void print(const int &&), which wouldn't make sense.

There is another case that I need to mention. When you pass a temp-value as a parameter, it is a &&. A temp-value is usually treated like a normal reference & in terms of template parameters. Here, for example, the compiler instantiates TYPE as Image&, even though this temp-value is actually an Image&&:

```
print(Image("my-image.png"));
```

Only when you write your template where the type parameter itself is qualified with && do you need to consider special cases—so very likely for the time being. If you believe you need to write such a template to manage your project, refer to the literature on