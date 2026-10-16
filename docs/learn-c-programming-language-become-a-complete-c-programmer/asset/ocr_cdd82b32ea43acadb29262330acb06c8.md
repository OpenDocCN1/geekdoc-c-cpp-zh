Probably, your first reaction is “But don’t do that!” and I agree. However, such code does get written, so it is worth knowing how it is interpreted.

A temporary **string** object is created to hold **s1+s2**. Next, a pointer to a C-style string is extracted from that object. Then – at the end of the expression – the temporary object is deleted. However, the C-style string returned by **c_str()** was allocated as part of the temporary object holding **s1+s2**, and that storage is not guaranteed to exist after that temporary is destroyed. Consequently, **cs** points to deallocated storage. The output operation **cout<<cs** might work as expected, but that would be sheer luck. A compiler can detect and warn against many variants of this problem.

The problem with the **if**-statement is a bit more subtle. The condition will work as expected because the full expression in which the temporary holding **s2+s3** is created is the condition itself. However, that temporary is destroyed before the controlled statement is entered, so any use of **cs** there is not guaranteed to work.

Please note that in this case, as in many others, the problems with temporaries arose from using a high-level data type in a low-level way. A cleaner programming style yields a more understandable program fragment and avoids the problems with temporaries completely. For example:

```
void f(string& s1, string& s2, string& s3)
{
  cout << s1+s2;
  string s = s2+s3;
  if (s.length()<8 && s[0]=='a') {
    // use s here
  }
}
```

A temporary can be used as an initializer for a **const** reference or a named object. For example:

```
void g(const string&, const string&);

void h(string& s1, string& s2) {
  const string& s = s1+s2; string ss = s1+s2;
  g(s,ss); // we can use s and ss here
}
```

This is fine. The temporary is destroyed when “its” reference or named object goes out of scope. Remember that returning a reference to a local variable is an error (§12.1.4) and that a temporary object cannot be bound to a non**const** lvalue reference (§7.7).

A temporary object can also be created explicitly in an expression by invoking a constructor (§11.5.1). For example:

```
void f(Shape& s, int n, char ch)
{
  s.move(string{n,ch}); // construct a string with n copies of ch to pass to Shape::move()
}
```