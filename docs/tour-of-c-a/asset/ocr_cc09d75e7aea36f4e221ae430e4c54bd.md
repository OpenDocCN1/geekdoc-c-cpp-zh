```
template<typename C, typename P>
int count(const C& c, P pred)
```

Il assume that C is a container and P is a predicate on its elements

```
{
  int cnt = 0;
  for (const auto& x : c) {
    if (pred(x))
      cnt++;
  }
  return cnt;
}
```

This is a simplified version of the standard-library count_if algorithm if §13.5.

Given objects (§8.2), we can formalize count()'s assumptions about its argument and check them at compile time.

A predicate is something that we can invoke to return true or false. For example:

Click here to view code image

```
void fcount(vector<int>& vec, const list<string>& lst, int x, const string& s) {
  cout << "number of values less than " << x << ": " << count(vec,x) << "in";
  cout << "number of values less than " << s << ": " << count(lst,Less_than(s)) << "in";
}
```

Here, Less_than(x) constructs an object of type Less_than<int>, which the call operator compares the value of the int called x; Less_than(s) constructs an object that compares to the value of the string called s.

The beauty of function objects is that they carry the value to be compared with (and type), and we don't have to introduce noisy global variables to hold values. Also, for a simple function object like Less_than, inlining is simple, a call of Less_than is far more efficient than an indirect call. The ability to carry data plus their efficiency makes function objects particularly useful as arguments to algorithms.

Function objects used to specify the meaning of key of a general algorithm (such as Less_than for count()) are sometimes referred to as policy objects.

# 7.3.3 Lambda Expressions

In §7.3.2, we defined Less_than separately from its use. That can be inconvenient. Consequently, there is a notation for implicitly generating function objects:

Click here to view code image

```
void fcount(vector<int>& vec, const list<string>& lst, int x, const string& s) {
  cout << "number of values less than " << count(vec,[](int a){return a < x;}) << "
";
  cout << "number of values less than " << count(lst,[](const string& a){return a < s;}) << "
";
}
```