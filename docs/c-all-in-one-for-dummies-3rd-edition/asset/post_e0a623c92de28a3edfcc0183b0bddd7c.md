
## Chapter 5: Creating Classes with Templates

### In This Chapter

- Creating class templates
- Using parameters in templates
- Deriving with templates
- Creating function templates

If C++ programming has any big secret, it would have to be templates. Templates seem to be the topic that beginning programmers strive to understand because they’ve heard about them and seem to think that templates are the big wall over which they must climb to ultimately become The C++ Guru.

We can’t say whether understanding templates will make you a C++ guru (we like to think that it will!), but we can say that it will open your abilities to a whole world out there, primarily because the entire Standard C++ Library is built around templates. Further, understanding templates can help you understand all that cryptic code that you see other people posting on the Internet. (And it will help you realize that it didn’t have to be so cryptic! Simplify, simplify, we always say!)

So, in this chapter, we show you how to use class templates in C++.

![](img/6ba99460b0feb3585671a4612ff5fabb_546_0.png)

Templates have an interesting history. Back when people started building C++ compilers, no standard for how to do templates existed. As a result, different compilers supported different ways of doing templates. The whole template thing was a mess and very confusing. So if you’re using a compiler that’s older than around 1999 or 2000 and you’re interested in using templates, you should seriously consider upgrading to a newer compiler (such as the GNU GCC compiler included with Code::Blocks).

### Templatizing a Class

“Templates are complicated and difficult to understand.” That was a lie. We don’t know why people think templates are so hard to create and use, but they’re really not. In this section, we show you just how simple templates are to understand.

For example, the following creates ten instances of the class, calls sum(), and prints the return value of sum():

```cpp
MyHolder *hold;
int loop;
for (loop = 0; loop < 10; loop++)
{
    hold = new MyHolder;
    hold->first = loop * 100;
    hold->second = loop * 110;
    hold->third = loop * 120;
    cout << hold->sum() << endl;
    delete hold;
}
```

This creates an instance at run time, does some work with it, and then deletes the instance. It then repeats this process over and over for a total of ten times. Instances (or variables) are created, changed, and deleted — all at run time. But the class, which we’ll say one more time, is created at compile time.

Suppose you're coding away, and you discover that this class MyHolder is pretty handy, except it would be nice if you had a version of it that holds floats instead of ints. You could create a second class just like the first that uses the word float instead of int, like this:

```cpp
class AnotherHolder
{
public:
    float first;
    float second;
    float third;
    float sum()
    {
        return first + second + third;
    }
};
```

This works the same way as the previous class, but it stores three float types instead of int types. But you can see, if you have a really big class, this method would essentially require a lot of copying and pasting followed by some search-and-replacing — in other words, busywork. But you can minimize this busywork by using templates. Instead of typing two different versions of the class, type one version of the class that you can, effectively, modify when you need different versions of the class.

Take a look at this code:

```cpp
template <typename T>
class CoolHolder
{
public:
    T first;
    T second;
    T third;
    T sum()
    {
        return first + second + third;
    }
};
```

Think of this as a rule for a class that does exactly what the previous two classes did. (Ignore the template declaration, `template <typename T>`, for now, it's explained a little later in the chapter.) In this rule is a placeholder called `T` that is a placeholder for a type. Imagine, in your mind, this set of code; then remove the first line and replace all the remaining `T`s with the word `int`. If you did that, you would end up with this:

```cpp
class CoolHolder
{
public:
    int first;
    int second;
    int third;
    int sum()
    {
        return first + second + third;
    }
};
```

This is, of course, the same as the earlier class called `MyHolder`, just with a different name. Now imagine doing the same thing but replacing each `T` with the word `float`. You can probably see where we're going with this. Here it is:

```cpp
class CoolHolder
{
public:
    float first;
    float second;
    float third;
    float sum()
    {
        return first + second + third;
    }
};
```

And once again, this is, of course, the same as the earlier class called `AnotherHolder`, but with a different name.

That's what a template does: It specifies a placeholder for a class. But it doesn't *actually create* a class ... yet. You have to do one more thing to tell the compiler to take this template and create a class. The way you do this is by writing code to create a variable or by using the class somehow. Look at this code:

```cpp
CoolHolder<int> IntHolder;
IntHolder.first = 10;
IntHolder.second = 20;
IntHolder.third = 30;
```

Do you see what’s happening? This code is telling the compiler to take the `CoolHolder` template and make a version of it where `T` is replaced by the word `int`. In other words, the compiler creates a class. What is the class called? It’s called `CoolHolder<int>`. And then these four lines of code first create an instance of `CoolHolder<int>` called `IntHolder`; then they set the members of `IntHolder`.

And when does the computer create this class? (That is, not the instance, but the class itself?) At compile time. Remember, types are created at compile time, and this is no exception to this rule.

![](img/6ba99460b0feb3585671a4612ff5fabb_550_0.png)

Here’s an easy way to look at a template. When you see a line like `CoolHolder<int> IntHolder;` you can think of it like `CoolHolderint IntHolder`. Although that’s not really what the template is called, you are telling the compiler to create a new class. In your mind, you may think of the class as being called `CoolHolderInt`, that is, a name without the angle brackets. (But remember that the name really isn’t `CoolHolderInt`. It’s `CoolHolder<int>`.)

The CoolHolder example shown in Listing 5-1 contains a complete application that uses the CoolHolder template.

### Listing 5-1: Using Templates to Create Several Versions of a Class

```cpp
#include <iostream>

using namespace std;

template <typename T>
class CoolHolder
{
public:
    T first;
    T second;
    T third;
    T sum()
    {
        return first + second + third;
    }
};

int main()
{
    CoolHolder<int> IntHolder;
    IntHolder.first = 10;
    IntHolder.second = 20;
    IntHolder.third = 30;

    CoolHolder<int> AnotherIntHolder;
    AnotherIntHolder.first = 100;
    AnotherIntHolder.second = 200;
    AnotherIntHolder.third = 300;

    CoolHolder<float> FloatHolder;
    FloatHolder.first = 3.1415;
    FloatHolder.second = 4.1415;
    FloatHolder.third = 5.1415;

    cout << IntHolder.first << endl;
    cout << AnotherIntHolder.first << endl;
    cout << FloatHolder.first << endl;

    CoolHolder<int> *hold;
    for (int loop = 0; loop < 10; loop++)
    {
        hold = new CoolHolder<int>;
        hold->first = loop * 100;
        hold->second = loop * 110;
        hold->third = loop * 120;
        cout << hold->sum() << endl;
        delete hold;
    }

    return 0;
}
```

When you run this application, you see a bunch of results from calls to `sum()`:

```text
10
100
3.1415
0
110
220
330
660
990
1320
1650
1980
2310
2640
2970
```

Look closely at the code. Near the beginning is the same template that we showed you earlier. Remember that the compiler doesn't create a type for this template. Instead, the compiler uses it as a rule to follow to create additional types. That is, the code indeed serves as a template for other types, thus its name.

Here's the first line of the template:

```cpp
template <typename T>
```

All this means is that a template class is going to follow, and that it has a type with a placeholder called `T`. That means that inside the class anywhere a `T` appears, it will be replaced by the typename. (The `T` is standalone; if you have it as part of a word, it won't be replaced.) The standard practice is for people to use `T` for the placeholder, but you can use any identifier (starting with a letter or underscore, followed by any combination of letters, numbers, or underscores).
