```
```cpp
int main() {
    infos<signed char>("char");              // smallest int type
    infos<short>("short");
    infos<int>("int");
    infos<long>("long");
    infos<long long>("long long");            // largest int type
}
```
```

**Listing 23.11** How to find the range of integer types.

Although this example is only designed for integer types, there are also many information functions for the float and double floating-point types.

# What Is “typename”?

> So far, you have only seen typename for template parameters—for example, before functions in `template<typename T>`. In such cases, you can also use class instead: `template<class T>` means exactly the same thing.
> 
> Since C++20, you can also use the name of a concept instead of typename to restrict the type of a template parameter. If infos is supposed to work only for integer types, use the `std::integral` concept from the `<concepts>` header instead of typename.
> 
> Outside of angle brackets, a typename appears exactly when you are writing a template and a type you are using is itself a template type in which you are using one of your template parameters. You can see this in Listing 23.11 at `typename std::numeric_limits<INT_TYP>`. Then you need the additional word typename before the name of the template type you are using. Otherwise, the compiler cannot know, before you assign a value/type to `INT_TYP`, whether `numeric<...>` is a variable, a type, or something else. You then have to tell it: “Hey, by the way, this is a type.”

# 23.3  A Class as a Function

So far, you can do two things with a function: you can define it, and you can call it. It becomes exciting and truly flexible only when you consider functions not just as a piece of outsourced program code but as objects like all other C++ objects. When you pass a function as a parameter, receive it as a return value, or simply store it in a variable for later use, you are using functions as objects.

I'll start with a very simple example. Say you want to write something that performs either an addition or a multiplication operation depending on a parameter. In the context of this chapter, I would like to call the thing that sometimes performs one operation and sometimes another a procedure to conceptually distinguish it from the variable function (addition or multiplication).