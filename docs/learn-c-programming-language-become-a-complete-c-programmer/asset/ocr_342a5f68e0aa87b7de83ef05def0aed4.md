later – maybe minutes later – a user presses the **draw triangle** button and the lambda tries to access the long-gone local variables. A lambda that wrote to a variable caught by reference would be even worse in that situation.

If a lambda might outlive its caller, we must make sure that all local information (if any) is copied into the closure object and that values are returned through the **return** mechanism (§12.1.4) or through suitable arguments. For the **setup()** example, that is easily done:

```
m.add("draw triangle",[=]{ m.draw(p1,p2,p3); });
```

Think of the capture list as the initializer list for the closure object and [=] and [&] as short-hand notation (§11.4.1).

# 11.4.3.2 Namespace Names

We don’t need to “capture” namespace variables (including global variables) because they are always accessible (provided they are in scope). For example:

```
template<typename U, typename V>
ostream& operator<<(ostream& os, const pair<U,V>& p)
{
return os << ‘{‘ << p.first << ‘,’ << p.second << ‘}’; }
void print_all(const map<string,int>& m, const string& label) {
cout << label << ":\n{\n";
for_each(m.begin(),m.end(),
[](const pair<string,int>& p) { cout << p << ‘\n’; });
cout << "}\n";
}
```

Here, we don’t need to capture **cout** or the output operator for **pair**.

# 11.4.3.3 Lambda and this

How do we access members of a class object from a lambda used in a member function? We can include class members in the set of names potentially captured by adding **this** to the capture list. This is used when we want to use a lambda in the implementation of a member function. For example, we might have a class for building up requests and retrieving results:

```
class Request {
function<map<string,string>(const map<string,string>&)> oper; // operation // arguments
// targets

map<string,string> values; map<string,string> results; public:
Request(const string& s); // parse and store request
void execute() {
[this]() { results=oper(values); } }
};
// do oper to values yielding results
```