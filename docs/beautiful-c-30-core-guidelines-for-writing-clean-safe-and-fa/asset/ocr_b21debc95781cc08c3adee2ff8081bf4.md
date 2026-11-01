The key there is “group relevant parts together,” which sounds to me a lot like “form an abstraction.” If you have state that is already related in some way, then formalize that relationship by defining a struct, and name, it in such a way as to capture and identify that relationship. Push the relevant functionality into the struct. Then you can replace those few lines of declarations with a single declaration: an instance of that struct. You should, at all times, remain vigilant for the opportunity to create a useful abstraction.

# Structured binding

There is an exception to this guideline, which applies when it comes to the use of structured bindings. This innovation was introduced in C++17, and allows you to bind an array or a nonunion class type to a list of names. For example, in the simplest case:

Click here to view code image

```
int a[2] = {1, 2};
auto [x, y] = a; // x = a[0], y = a[1]
```

Binding to a tuple like type is also simple:

Click here to view code image

```
std::unordered_map<std::string, int> dictionary;
auto [it, flag] = dictionary.insert({"one", 1});
// it points to the element
// flag signals whether the insertion was successful
```

Binding to a struct to unpack it works in the same way:

Click here to view code image

```
struct s {
    int a;
```