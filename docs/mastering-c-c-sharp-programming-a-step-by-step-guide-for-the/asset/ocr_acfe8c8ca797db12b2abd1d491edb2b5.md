```
{
	Console.WriteLine(x);
}
```

```
for(int x = 50; x < 60; x++)
{
	Console.WriteLine(x);
}
```

The first scope type we looked at was called method scope but this one is called block or inner block scope.

The key is to allow the curly braces to guide you. Whatever is created inside the curly braces is usable anywhere within them.

The next logical step from here is the class scope. Take a look at the variable instances; they are set inside the curly braces and are usable within the class and that includes our constructors and the methods that we will be creating shortly.

# Name Hiding

There is one thing that C# allows you to do – if you have a local variable with block or method scope or a parameter, you can give it the same name as something with class scope. When we created our class, we created an instance variable that we called name – this has class scope because it can be used throughout the class. Then we had a parameter within the constructor that we also called name and this has method scope because it can only be used in the method or constructor.

This creates something known as name hiding. While we can use the instance variable called name within the class, including our constructor, there is now another one on the constructor that has the same name and is also usable. Which one are we referring to when