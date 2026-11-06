The first call uses a previously declared variable of type `MyNumber`. The second call creates a temporary instance, passing the value 23 into the constructor. The third one also creates a temporary instance, but it does so implicitly! The output from this example is

```
17
23
29
```

You may wonder when your temporary variables get destroyed. For instance, if you call `WriteNumber(MyNumber(23));`, how long does the temporary `MyNumber` instance live on? The ANSI standard proudly proclaims that the instance will get deleted at the end of the *full expression*. In other words, after the line is done, the temporary instance will be done for.

![](bbox=[0.143, 0.272, 0.228, 0.343])

Be careful when using implicit temporary objects. Consider the following class and function found in the `Constructor07` example:

```
class MyName
{
public:
    string First;
    MyName(string TheFirst) : First(TheFirst) {}
};

void WriteName(MyName name)
{
    cout << "Hi I am " << name.First << endl;
}
```

Seems straightforward. The `MyName` constructor takes a string, so it seems like we should be able to do this when we call the `WriteName()` function:

```
WriteName("George");
```

Except we can’t. The compiler gives us an error message:

```
In function 'int main()':
error: could not convert '(const char*)"George"' from 'const char*'
    to 'MyName'
```

Here’s the problem: The compiler got shortsighted. The compiler considers the type of the string constant a `const char *` (that is, a pointer to a const character, or really a constant character array). Although we don’t have any constructors that take a `const char *` parameter, we do have one that takes a string, and it has a constructor that takes a `const char *` parameter. Unfortunately, the compiler doesn’t fall for that, and it complains. So we have to adjust our function call just a tad, like so:

```
WriteName(string("George"));
```