Herein lies a potential maintenance issue. Although you're typing less code, you have to balance this with the additional effort required when someone else has to maintain your code, because it's no longer clear which class each belongs to. IntelliSense in Visual Studio helps to some extent, but to a developer reading through the code and trying to track down the cause of a bug, it can obfuscate matters. So, use static statements carefully. (My preferred style is not to use them, although you are free to make your own choice!)

In the final exercise in this chapter, you'll add a static field to the Point class and initialize the field to o. You will increment this count in both constructors. Finally, you will write a public static method to return this private static field. With this field, you can discover how many Point objects you have created.

# To write static members and call static methods

+   1. In Visual Studio 2022, display the Point class in the Code and Text Editor window.

+   2. Add a private static field called oldCount of type int to the Point class immediately before the first constructor and initialize it, like this:

Click here to view code image

```
class Point
{
    private int x, y;
    private static int oldCount = 0;

    public Point()
    {
        ...
    }
}
```

> > **Note**
>---\-
> You can write the keywords private and static in any order when you declare a field such as oldCount. However, the preferred order is private first, static second.