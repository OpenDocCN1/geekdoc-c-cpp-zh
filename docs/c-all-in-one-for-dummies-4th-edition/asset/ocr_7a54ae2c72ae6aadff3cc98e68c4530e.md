# THE STRING CLASS

If you've been reading the previous chapters of Book 1 (and now this first chapter of Book 2), and trying the applications, you have seen the string type. Now for the big secret: string is actually a class. When you create a variable of type string, you are creating an object of class string. That's why, to use the string functions, you first type the variable name, a dot, and then the function name: You are really calling a method for the string object that you created. Similarly, when you work with pointers to strings, instead of a dot you can use the → notation to access the methods. (See "Using classes and raw pointers," later in this chapter, for more information.) When working with newer versions of C++, the string class is part of the std namespace, which is why you add `using namespace std;` to the beginning of your code. If you use an older version of C++, the string class appears as part of the string file. In this case, you include `<string>` to provide the necessary header files to declare the string class.

This line outputs the InkColor member for FavoritePen. But what type is InkColor? It’s the new Color enumerated type. But something is wrong. It printed 0 despite being set as follows:

```
```cpp
FavoritePen.InkColor = blue;
```
```

The code sets it to blue, not 0. Unfortunately, that’s the breaks with using enum. You can use it in your code, but under the hood, it just stores numbers. When printed, you get a number. The compiler chooses the numbers for you, and it starts the first entry in the enum list as 0, the second as 1, then 2, then 3, and so on. Thus, blue is stored as 0, red as 1, black as 2, clear as 3, and grey as 4. Fortunately, people have found a way to create a new class that handles the enum for you (that is, it wraps around the enum), and then you can print what you really want: blue, red, black, clear, and grey. Book 2, Chapter 2 has tips on how to do this astounding feat.

![](bbox=[0.175, 0.697, 0.231, 0.762])

Remember that you can create several objects (also called instances) of a single class. Each object gets its own properties, which you declare in the class. To access the members of an object, you use a period, or dot.

# Separating method code

When you work with functions, you can either make sure that the code to your function is positioned before any calls to the function, or you can use a *forward reference*, also called a *function prototype*. Book 1, Chapter 6 discusses this feature.