```
else
cout q->second;
```

In fact, [] is little more than a convenient notation for insert(). The result of m[k] is equivalent to the result of (* (m.insert(make_pair(k,V{})).first)).second, where V is the mapped type.
The insert(make_pair()) notation is rather verbose. Instead, we could use emplace():

```
dictionary.emplace("sea cow","extinct");
```

Depending on the quality of the optimizer, this may also be more efficient.
If you try to insert a value into a map and there already is an element with its key, the map is unchanged. If you want to have more than one value for a single key, use a multimap.

The first iterator of the pair (§34.2.4.1) returned by equal_range() is lower_bound() and the second upper_bound(). You can print the value of all elements with the key “apple” in a multimap<string,int> like this:

```
multimap<string,int> mm {{"apple",2}, {"pear",2}, {"apple",7}, {"orange",2}, {"apple",9}};
```

```
const string k {"apple"};
auto pp = mm.equal_range(k);
if (pp.first==pp.second)

cout << "no element with value " << k << "\n";
else {
cout << "elements with value " << k << ":\n";
for (auto p=pp.first; p!=pp.second; ++p)
cout << p->second << ' ';
}
```

This prints 279.
I could equivalently have written:

```
auto pp = make_pair(m.lower_bound(),m.upper_bound());
// ...
```

However, that would imply an extra traversal of the map. The equal_range(), lower_bound(), and upper_bound() are also provided for sorted sequences (§32.6).
I tend to think of a set as a map with no separate value_type. For a set, the value_type is also the key_type. Consider:

```
struct Record {
string label;
int value;
};
```

To have a set<Record>, we need to provide a comparison function. For example:

```
bool operator<(const Record& a, const Record& b)
{
```