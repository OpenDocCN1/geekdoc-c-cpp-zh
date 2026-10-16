```
void print(const vector<T>& v) {
for (auto& x : v)
cout << v << ' ';
cout << '\n';
void f()
{
std::vector<int> v {7, 3, 9, 4, 0, 1};
sort(v);
print(v);
sort(v,[](int x, int y) { return x>y; });
print(v);
sort(v.begin(),v.end());
print(v);
sort(v.begin(),v.end(),[](int x, int y) { return x>y; });
print(v);
}
```

The namespace lookup rules and the overloading rules for templates ensure that we find and invoke the correct variants of sort() and get the expected output:

```
013479
974310
013479
974310
```

If we removed the using namespace std; from E std, this example would still work because std’s sort()s would be found by argument-dependent lookup (§14.2.4). However, we would then not find the standard sort()s for our own containers defined outside std.

# 14.4.6 Versioning

The toughest test for many kinds of interfaces is to cope with a sequence of new releases (versions). Consider a widely used interface, say, an ISO C++ standard header. After some time, a new version is defined, say, the C++11 version of the C++98 header. Functions may have been added, classes renamed, proprietary extensions (that should never have been there) removed, types changed, templates modified. To make life “interesting” for the implementer, hundreds of millions of lines of code are “out there” using the old header, and the implementer of the new version cannot ever see or modify them. Needless to say, breaking such code will cause howls of outrage, as will the absence of a new and better version. The namespace facilities described so far can be used to handle this problem with very minor exceptions, but when large amounts of code are involved, “very minor” still means a lot of code. Consequently, there is a way of selecting between two versions that simply and obviously guarantees that a user sees exactly one particular version. This is called an inline namespace:

```
namespace Popular {
```