not really about function overloading in C++. Nonetheless, we discuss some of them here in part because they apply somewhat more often than other rules and in part to provide a sense for how deep the details go.

# C.3.1 Prefer Nontemplates or More Specialized Templates

When all other aspects of overload resolution are equal, a nontemplate function is preferred over an instance of a template (it doesn’t matter whether that instance is generated from the generic template definition or whether it is provided as an explicit specialization). For example: Click here to view code image

```
template<typename T> int f(T); // #1
void f(int); // #2

int main()
{
return f(7); // ERROR: selects #2 , which doesn’t return a value
}
```

This example also clearly illustrates that overload resolution normally does not involve the return type of the selected function.

However, when other aspects of overload resolution slightly differ (such as having different const and reference qualifiers), first the general rules of overload resolution apply. This effect can easily accidentally cause surprising behavior, when member functions are defined that accept the same arguments as copy or move constructors. See Section 16.2.4 on page 333 for details.

If the choice is between two templates, then the most specialized of the templates is preferred (provided one is actually more specialized than the other). See Section 16.2.2 on page 330 for a thorough explanation of this concept. One special case of this distinction occurs when two templates only differ in that one adds a trailing parameter packs: The template without the pack is considered more specialized and is therefore preferred if it matches the call. Section 4.1.2 on page 57 discusses an example of this situation.

# C.3.2 Conversion Sequences