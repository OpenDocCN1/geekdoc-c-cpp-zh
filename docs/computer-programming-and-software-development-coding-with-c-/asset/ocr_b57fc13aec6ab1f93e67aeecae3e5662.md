# Chapter 13 Named Arguments & Optional Parameters

Can we just randomly leave out an argument when calling a method? Well, yes and no. Let me explain. Using optional parameters, it's possible for us when creating a method to specify a default value in the parameter list for one or more parameters. When we then invoke the method, it's possible to leave out the optional ones, and then the method will rely on the default that we have defined. Let me show you a small snippet with optional parameters. In the snippet on the left, I have defined an optional parameter.

```
public int AddNumbers
    (int a, int b, int c = 100)
{
    int sum = a + b + c;
    return sum;
}
```

Notice that I have added a default value for the third parameter, so the c. That is now an optional parameter. We don't need to add another keyword here or something to make it optional. By just adding a default value, C# knows that it needs to use the default value if we omit it. Here, I'm calling this method.

```
AddNumbers(10, 20);//no third parameter
AddNumbers(10, 20, 30);
```