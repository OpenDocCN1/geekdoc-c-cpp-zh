![](bbox=[0.163, 0.094, 0.226, 0.159])

A single `<` function may not seem like enough to perform all the required comparisons, such as equality. However, the code calls the less-than function twice, the second time flip-flopping the order of the parameters; and if the function returns false both times, the computer determines that they are equal. Using this approach makes life easier because you need to provide only a single comparison function.

# UNDERSTANDING THE DEFAULT `<` FUNCTION

Containers in the Standard Library have a default `<` function. If you don’t supply a `<` function of your own, the container supplies this default `<` function for you. This default function relies on a template class called less. This template is simple: It includes a single method that returns the Boolean value:

`x < y`

For most basic types, the default works fine. For example, the compiler can easily use the default when you’re working with integers. However, the compiler doesn’t understand the `<` operator when working with custom classes unless you provide your own `<` operator function, as you see everywhere else in this chapter. However, because the container takes a class in its parameter that defaults to the class less, you can put together your own class and use that instead of writing your own `<` operator function. Here’s a sample:

```
class MyLess {
public:
  bool operator()(const MyClass &x, const MyClass &y) const {
    return x.Name < y.Name;
  }
};
```

Then when you create, for example, a map, you pass this class as a third parameter, rather than relying on the default:

`map<MyClass, MyClass, MyLess> mymap;`

Then you don’t need your own less-than function. The advantage of this approach is that you now have a standardized `<` function implementation to use everywhere, and it’s especially helpful when working within a team environment.