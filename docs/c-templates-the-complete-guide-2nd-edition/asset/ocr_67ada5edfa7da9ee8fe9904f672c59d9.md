# 17.8 Type Checking for Templates

Much of the complexity of programming with templates comes from the compiler’s inability to locally check whether a template definition is correct. Instead, most of the checking of a template occurs during template instantiation, when the template definition context and the template instantiation context are intertwined. This mixing of different contexts makes it hard to assign blame: Was the template definition at fault, because it used its template arguments incorrectly, or was the template user at fault, because the supplied template arguments didn’t meet the requirements of the template? The problem can be illustrated with a simple example, which we have annotated with the diagnostics produced by a typical compiler: Click here to view code image

```
template<typename T>
T max(T a, T b)
{
return b < a ? a : b;
// ERROR: "no match for operator <
// (operator types are ‘X’ and ‘X’)"
}

struct X {
};
bool operator> (X, X);

int main()
{
X a, b;
X m = max(a, b); // NOTE: "in instantiation of function template specialization
// ‘max<X>’ requested here"
}
```

Note that the actual error (the lack of a proper operator<) is detected within the definition of the function template max(). It is possible that this is truly the error—perhaps max() should have used operator> instead? However, the compiler also provides a note that points to the place that caused the instantiation of max<X>, which may be the real error—perhaps max() is documented to require operator<? The inability to answer this question is what often leads to the “error novel” described in Section 9.4 on page 143, where the compiler provides the entire template instantiation history from the initial cause of the instantiation down to the actual template definition in which the error was detected. The programmer is then expected to determine which of the template definitions (or perhaps the original use of the template) is actually in error.