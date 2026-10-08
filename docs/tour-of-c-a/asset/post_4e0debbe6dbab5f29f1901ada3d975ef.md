
Click here to view code image

```cpp
template<typename C, typename V>
vector<typename C::iterator> find_all(const C& c, V v)
{
    vector<typename C::iterator> res;
    for (auto p = c.begin();p!=c.end(); ++p)
        if (*p==v)
            res.push_back(p);
    return res;
}
```

It find all occurrences of v in c

The typename is to inform the compiler that C's iterator is supposed to be a type and not of some value type, the integer 7.
Alternatively, we could have returned a version of ordinary pointers to the elements:

Click here to view code image

```cpp
template<typename C, typename V>
auto find_all(const C& c, V v)
{
    range_value_t<C>* res;
    for (auto& x : c)
        if (x==v)
            res.push_back(&x);
    return res;
}
```

It find all occurrences of v in c

While I was at, I also simplified this by using a range-for loop and the standard-library range_value_t (§16:4) to name the type of the elements. A simplified version of range_value_t can be defined like this:

Click here to view code image

```cpp
template<typename T>
using range_value_type_t = T::value_type;
```

Using either version of find_all(), we can write:

Click here to view code image

```cpp
void test()
{
    string m = "Mary had a little lamb";
    for (auto p : find_all(m, 'a'))
        if (*p == "a")
            cerr << "string bug";
}
```

It p is a string::iterator

-   list<int> id {1, 2, 3, 1, -11, 2};
for (auto p : find_all(id,1))
    if (*p!=1)
        cerr << "list bug";

It p is a list<int>::iterator

```cpp
vector<string> vs = {"red"};
```

It p is a vector<string>::iterator

```cpp
cerr << "vector bug\n";

for (auto p : find_all(vs))
```

Iterators are used to separate algorithms and containers. An algorithm operates on its data through iterators and knows nothing about the container in which the elements are stored. Conversely, a container knows nothing about the algorithms operating on its elements; all it does is to supply iterators upon request (e.g., begin() and end()). This model of separation between storage and algorithm delivers very general and flexible software.

![](img/0bd2e25eba2737c3c5daca16fad1b65b_195_0.png)

# 13.3 Iterator Types

What are iterators really? Any particular iterator is an object of some type. There are, however, many different iterator types—an iterator needs to hold the information necessary for doing its job for a particular container type. These iterator types can be as different as the containers and the specialized needs they serve. For example, a vector's iterator could be an ordinary pointer, because a pointer is quite a reasonable way of referring to an element of a vector:

![](img/0bd2e25eba2737c3c5daca16fad1b65b_195_1.png)

Alternatively, a vector iterator could be implemented as a pointer to the vector plus an index:

![](img/0bd2e25eba2737c3c5daca16fad1b65b_195_2.png)

Using such an iterator allows range checking.
A list iterator must be something more complicated than a simple pointer to an element because an element of a list in general does not know where the next element of that list is. Thus, a list iterator might be a pointer to a link:

iterator:

| list: | link | link | link | ... |
| --- | --- | --- | --- | --- |
| elements: | P | i | e | t |

What is common for all iterators is their semantics and the naming of their operations. For example, applying ++ to any iterator refers to the next element. Similarly, * yields the element to which the iterator refers. In fact, any object that obeys a few rules like this is an iterator. *Iterator* is a general idea, a concept (§8.2), and different kinds of iterators are available as standard-library concepts, such as forward_iterator and random_access_iterator (§14.5). Furthermore, users need to know the type of a specific iterator; each container “knows” its iterator types and makes them available under the conventional names iterator and const_iterator. For example, list<Entry>::iterator is the general iterator type for list<Entry>. We rarely have to worry about the details of how that type is defined

In some cases, an iterator is not a member type, so the standard library offers iterator_t<X> that works where X’s iterator is defined.

# 13.3.1 Stream Iterators

Iterators are general and useful concepts for dealing with elements in containers. However, containers are not the only place where we find sequences of elements. For example, an input stream produces a sequence of values, and we write a sequence of values to an output stream. Consequently, the notion of iterators can be usefully applied to input and output.

To make an ostream_iterator, we need to specify which stream will be used and the type of objects written to it. For example:

Click here to view image

```cpp
ostream_iterator<string> oo (cout); // write strings to cout
```

The effect of using ++oo is to write the assigned value to cout. For example:

Click here to view image

```cpp
int main() {
  oo = "Hello, ";
  ++oo;
  oo = "world!\n";
  cout << "Hello, ";
}
```

This is another way of writing the canonical message to standard output. ++oo is done to mimic writing iterator through a pointer. That way, we can use algorithms on streams. For example:

Click here to view image

```cpp
vector<string> v("Hello", "World!\n"); copy(v, oo);
```

Similarly, istream_iterator is something that allows us to treat an input stream as a read-only container. Again, we must specify the stream to be used and the type of values expected:

Click here to view image

```cpp
istream_iterator<string> ii(cin);
```

Input iterators are used in pairs representing a sequence, we must provide an istream_iterator to indicate the end of the input. This default is istream_iterator:

```cpp
istream_iterator<string> eos();
```

Typically, istream_iterators and ostream_iterators are not used directly, they are provided as arguments to algorithms. For example, we can write a simple program to read a file, sort the words, eliminate duplicates, and write the result to another file:

Click here to view image

```cpp
int main()
{
    string from, to;
    cin >> from >> to;

    if (ifstream(from)) {
        istream_iterator<string> ii(from);
        istream_iterator<string> eos(cin);
    }

    if (ofstream(to)) {
        ostream_iterator<string> os(to, "\n");

        vector<string> b(ii, eos);
        sort(b);

        unique_copy(b.begin(), b.end(), os);

        return;
    }
}
```

I used the range versions of sort() and unique_copy(). I could have used iterators, e.g., sort(b.begin(),b.end()), which is as order. Please remember to use both a traditional iterator version of a standard-algorithm and its counterpart, we need to either qualify the call of range version or use a declaration (§9.3.2):

Click here to view image

```cpp
copy(v, oo); // potentially ambiguous
ranges::copy(v, oo); // OK
using ranges::copy(v, oo); // copy(v, oo) OK
```

If istream is an istream that can be attached to a file (§11.7.2), and an ostream is an ostream that can be attached to a file. The ostream_iterator's second needs to be. We read the strings into a vector, then we sort() them, and we write them out, eliminating duplicates. A more elegant solution is not to store duplicates at all. This can be done by keeping the strings in a set, which does not keep duplicates and keeps its elements in order (§12.5). That way, we could replace the two lines using a vector for a set and replace unique_copy() with the simpler copy():

Click here to view image

```cpp
set<string> b(ii,eos);      // collect strings from input
copy(b,o);               // copy buffer to output
```

We used the names ii, eos, and oo only once, so we could further reduce the size of the program:

Click here to view image

```cpp
int main() {
    string from, to;
    cin >> from >> to;        // get source and target file names
    if (istream(from)) {    // input stream for "from"
        ostream << to;          // output stream for "to"
    }
    set<string> b(istream_iterator<string>(is),istream_iterator<string>()); // read input
    copy(b,ostream_iterator<string>(os,""));                           // copy to output
    return !is.eof() || os;   // return error (§1.2.1, §11.4)
}
```

It is a matter of taste and whether or not this simplification improves readability.

# 13.4 Use of Predicates

In the examples we have “built in” the action to done for each element of a sequence. We often want to make that action a parameter to the algorithm. For example, the find (§13.2, §13.5) provides a convenient way of looking for a specific value. A more general variant like we might want to search a map for the first value larger than 42. A map allows us to access its elements as a sequence of (key,value) pairs, so we can search for a map<string,const_int> where the int is greater than 42.

Click here to view code image

```cpp
void f(map<string,int>& m) {
    auto p = find_if(m.begin(), m.end(), Greater_than(42));
    //...
}
```

Here, Greater_than is a function (§7.3.2) holding the value (42) to be compared against a map entry of type pair<string,int>:

Click here to view code image

```cpp
struct Greater_than {
    int val;
    Greater_than(int v) : val(v) {
```
