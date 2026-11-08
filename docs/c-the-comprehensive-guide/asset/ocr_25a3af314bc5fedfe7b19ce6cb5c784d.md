Therefore, instead of writing

```
```cpp
return Person{name, age, city};
```
```

simply write

```
```cpp
return {name, age, city};
```
```

The compiler knows from the return type of the function that you want to create a Person, so it tries to convert the list you provided into a Person; the two expressions are almost synonymous. You can choose which style you prefer.

There are cases where you need to specify Person{...}—for example, when using the syntax for function declaration available since C++14, auto create(). The next listing shows an example.

```
```cpp
// https://godbolt.org/z/jer44aWs9
auto create(string name, int age, string city) {
    return Person{name, age, city};  // auto requires constructor name
}
auto create2(string name, int age, string city) {
    return {name, age, city};        // auto with initializer_list does not work
}
```
```

**Listing 12.4** Here, specifying Person in the return is necessary.

Here, an initializer_list is returned in create2. That would be fine if you had specified a return type in the function header into which the initializer_list can be automatically converted. But here it says auto, and the compiler cannot infer the type from that.

# 12.3 Methods Instead of Functions

The print function in Listing 12.1 requires a Person to work; it is in fact specifically designed for Person and nothing else. It might even be the case that the Person type only really makes sense if you also provide a suitable set of functions that work with your new type.

These functions, along with the data in struct Person, belong to the interface of this type. It is a pity that print is not already listed in the Person type—but you can do exactly this. Combine the functions of a type with the data to form an entity such that neither can exist without the other. Such a function always requires a variable, and a variable without the associated functions is almost useless.¹ A variable that is part of

¹ The static methods that do not require instance variables will be covered later.