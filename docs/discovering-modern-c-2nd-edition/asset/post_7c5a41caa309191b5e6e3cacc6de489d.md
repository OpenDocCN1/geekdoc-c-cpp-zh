
the tuple. This is often more elegant. In this case, we have to declare compatible variables beforehand:

```
matrix LU;
vector p;
tie(LU, p) = lu(A);
```

tie looks quite mysterious at first but its implementation is surprisingly simple: it creates an object with references to function arguments. Assigning a tuple to that object performs assignments of each tuple member to the respective reference.

The implementation with tie has a performance advantage over the implementation with get. When we pass the result of function lu directly to tie, it is still an rvalue (it has no name) and we can move the entries. With an intermediate variable, it becomes an lvalue (it has a name) and the entries must be copied. To avoid the copies, we can also move the tuple entries explicitly:

```
auto t = lu(A);
auto LU = get<0>(move(t));
auto p = get<1>(move(t));
```

Here, we step on rather thin ice. In principle, an object is considered expiring after move is applied on it. It is allowed to be in any state as long as the destructor doesn't crash. In our example, we read t again after using move upon it. This is not correct in this special situation. move turns t into an rvalue and we can do whatever we want to its data. But we don't. When LU is created, we only take the data of the tuple's entry 0 and don't touch entry 1. Conversely, we only steal the data from t's entry 1 in p's creation and don't access the expired data in entry 0. Thus, the two moves move entirely disjointed data. Nonetheless, multiple occurrences of move on the same data item are very dangerous and must be analyzed carefully (as we did). We can simply relieve ourselves from these worries by moving the single members instead:

```
auto LU = move(get<0>(t));
auto p = move(get<1>(t));
```

C++17 Since C++17 we can use type deduction without storing the tuple:

```
auto [LU, p] = lu(A);
```

Not only is this simpler and clearer, it is even more efficient. For such examples we observed that modern compilers are able to apply copy elision to the tuple components so that LU and p are neither copied nor moved.

The other heterogeneous class in C++ is pair. It already existed in C++03 and still does. pair is equivalent to a tuple with two arguments. Conversions from one to another exist so pair and two-argument tuple can be exchanged with each other and even mixed. The examples in this section could all be implemented with pair. Instead of get<0>(t) we could also write t.first (and t.second for get<1>(t)).

## C++17 4.4.3 variant

=> c++17/variant_example.cpp

variant is the modern version of a classic C++ feature called union that we omitted for good reasons. There are two kinds of unions: one is pretty dangerous and the other much more dangerous.

The purpose of variant is to have objects that can store values of different types. In our program we choose a set of types, for instance int, double, and string, and a variant object can store any value of those types:

Click here to view code image

```
using my_variant = variant<int, double, string>;
my_variant var;
```

```
var = 3;
var = 4.2;
var = "Text";
```

We can access the value with get and an (zero-based) index. In var above, the string has index 2:

```
string s = get<2>(var);
```

To not bother with the order of types, we can use the type instead of the index:

```
s = get<string>(var);
```

If we tried to access the wrong type or index, e.g.:

```
int i = get<int>(var); // Error at run time
```

an exception of type `bad_variant_access` is thrown.

The special charm of `variant` shows up when we refrain from explicitly dispatching between the possible types of the values and leave this to function overloading. Assume we have a container of our `variant` type and we like to count how many objects of each possible value type are stored, and for no specific reasons we like to guess how many symbols would be written to a stream if we printed the entire container (we know there are simpler ways to do this). We first create a simplistic `record` class:

```
struct record
{
    int counted_ints = 0,
           counted_doubles = 0,
           counted_strings = 0,
           total_symbols = 0;
};
```

Then we create a functor `symbol_counter` that refers the `record` and overloads the application operator for our value types:

Click here to view code image

```
struct symbol_counter
{
    symbol_counter(record& r) : r(r) {}

    void operator()(int i) const
    {
        r.counted_ints++;
        r.total_symbols += floor(log10(i)) + 1;
    }

    void operator()(double d) const
    {
        r.counted_doubles++;
        r.total_symbols += 15;
    }

    void operator()(const string & s) const
    {
        r.counted_strings++;
        r.total_symbols += s.size();
    }

private:
    record& r;
};
```

Each `operator()` increments the according counter and adds its estimation for additional symbols. For a given container:

![](img/5682e787fc967e93d7e33e8bac5f58a0_406_0.png)

```
vector<my_variant> v = {33, 2.3, "Huhu ", "Dings"s, 11111,
 3.809};
```

We can count the objects and symbols with a simple loop:

```
record r;
symbol_counter sc{r};
for (const auto& mv : v)
 visit(sc, mv);
```

The functor `symbol_counter` is called for each entry of our vector and the right overload of `operator()` is called based on the value type that the current `variant` object holds. If we omitted the `string` overload, the code wouldn't compile anymore.

We hope this demonstration convinced you of `variant`'s type safety: not only can we not access a value with the wrong type, we are also forced to provide functors that can handle all possible value types—regardless of whether a missing type is actually used at run time. A nerdier and shorter but somewhat less comprehensible version is found in Section A.7.2.

## C++17 4.4.4 any

`any` is a utility class (in `<any>`) for storing objects of copy-constructible classes by type erasure:

```
any a;
a = 3;
a = 4.2;
```

Disrespectfully we could say it is an improved `void*`. In contrast to `void*`, an object isn't just referred but a copy of it is held. We can thus fill a container with objects without the need of keeping the original objects for the container's validity:

![](img/5682e787fc967e93d7e33e8bac5f58a0_406_1.png)

```
vector<any> v = {33, 2.3, "Huhu "s, "Dings"s, 11111, 3809,
"Soso"};
v.push_back(42.0);
```

Although an `any` object can hold any copyable object it is still type-safe because it keeps the currently stored object's type-id. To retrieve the stored object, we must know its type and provide it to `any_cast`:

Click here to view code image

```
cout << "a is " << any_cast<double>(a) << ".\n";
```

If the type is wrong, an exception of type `bad_any_cast` is thrown. We can also request the current type-id with `type`, for instance to filter all `int` values from a `vector<any>`:

Click here to view code image

```
auto find_ints(const vector<any>& v)
{
    vector<int> vi;
    for (const any& a : v)
        if (a.type() == typeid(int))
            vi.push_back(any_cast<int>(a));
    return vi;
}
```

The type `any` is probably nothing we want in the innermost kernel of a high-performance application but whenever we need to collect sufficiently diverse objects (e.g., building a data warehouse) it simplifies our work considerably.

## C++17 4.4.5 string_view

=> c++17/string_view2.cpp

A `string_view` is a lightweight handle to refer a `string` or a `char` array for read-only use. Both string types can be implicitly converted to `string_view`:

Click here to view code image

```
void print_some_string(string_view sv)
{
    cout << sv << '\n';
}
```

```
print_some_string("const char*");
print_some_string("string"s);
```

As the type typically consists of only a pointer and a size value, its objects can therefore be passed by value. Not owning the memory is a blessing and a curse. The curse is that we can refer obsolete data if we don't pay attention. Say we want to concatenate two string_view objects. Since they are immutable, we convert both to string first and concatenate those:

Click here to view code image

```
namespace std {
string operator+(string_view v1, string_view v2)
{
    return string{v1} + string{v2};
}
}
```

Assume further that we have a generic function twice that adds an object to itself:

```
template <typename T>
T twice(T x)
{
    return x + x;
}
```

This innocent-looking little function works with all types we used so far but not with string_view. Our self-defined operator+ returns a string and we convert it to a string_view when we return the result of twice. Our result refers to the correctly concatenated string but that string is a temporary in the function which is destroyed at function end. Thus, the returned string_view contains a stale reference. This problem can be easily solved by replacing the return state with auto. When storing the result, it shouldn't be a string_view either as this contained a stale reference to a temporary string; auto comes in handy again. The tricky part is to find out what is going wrong in this situation; and this is much harder in a large code base.

The upside of not owning the memory is that it can be used very efficiently to represent sub-strings. As a string_view is not required to be 0-terminated, we can even use it for old C strings, but this book is about modern C++, not antique C. Say we have a string with 100,000 letters and want to refer the first half of it:
