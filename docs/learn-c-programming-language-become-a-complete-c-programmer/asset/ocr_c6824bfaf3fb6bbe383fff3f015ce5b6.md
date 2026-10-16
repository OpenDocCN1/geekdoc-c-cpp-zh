```
class Xrefd2 {
C mems;
C2 refs;
// ...
};
Xrefd2<vector<Entry>,set<Entry *>> x;
```

Here, the value types of C and C2 can be obtained by a simple type function (§28.2) for obtaining the type of elements of a container, for example, Value_type<C>. This is the technique used for the standard-library container adaptors, such as queue (§31.5.2).

# 25.2.5 Default Template Arguments

Explicitly specifying the comparison criterion for each use of map is tedious – especially as less<Key> is typically the best choice. We can specify less<Key> to be the default type for the Compare template argument, so that only uncommon comparison criteria have to be explicitly specified:

# Section 25.2.5 Default Template Arguments 729

```
template<typename Key, Class V, typename Compare = std::less<Key>> class map {
public:
explicit map(const Compare& comp ={});
// ...};
map<string,int> m1;
map<string,int,less<string>> m2;
```

```
struct No_case { // define operator()() to do case-insensitivestringcomparison
};
// will use less<string> for comparisons // same type as m1
map<string,int,No_case> m3; // m3 is of a different type from m1 and m2
```

Note how the default map constructor creates a default comparison object, Compare{}. That’s the common case. If we want a more elaborate construction, we must do so explicitly. For example:

```
map<string,int,Complex_compare> m {Complex_compare{"French",3}};
```

The semantic checking of a default argument for a template parameter is done only if that default argument is actually used. In particular, as long as we refrain from using the default template argument less<Key>, we can compare() values of a type X for which less<X> wouldn’t compile. This point is crucial in the design of the standard containers (e.g., std::map), which rely on a template argument to specify default values (§31.4).

Just as for default function arguments (§12.2.5), the default template arguments can be specified and supplied for trailing arguments only:

```
void f1(int x = 0, int y); // error :default argument not trailing
void f2(int x = 0, int y = 1); // OK
f2(,2); // syntax error f2(2); // call f(2,1);
template<typename T1 = int, typename T2>
```