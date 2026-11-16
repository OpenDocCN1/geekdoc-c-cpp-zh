However, it would have been legal (and is usually preferred) to initialize all the data members in the constructor initializer list as follows:

```
Counter (int init, int size) : count(init), MAX(size) {}
```

# True Constants Inside Classes

The treatment of const inside classes creates an inconvenient situation when you're creating an array inside a class. When dealing with ordinary arrays (not inside classes) the best programming practice is to use a named constant to define the size of the array:

```
const MAX = 10;
int num[MAX];
```

This way, any code that refers to the size of the array uses MAX and if you need to change the value of MAX, you only change it in one place, at the const definition.

However, you cannot use a const data inside an array definition within a class because the compiler must know the size of the array when it is defined and because a const inside a class always allocates storage (the compiler cannot know the contents of a storage location). So the following is illegal:

```
class Array {
private:
    const int MAX;
    int num[MAX];
};
```

Fortunately, there is a convenient way to work around the problem. The enumerated data type enum is designed to associate names with integral numbers. Normally enum is used to distinguish a set of names by letting the compiler automatically assign numbers to them. However, you can force a name to be associated with a particular number by: