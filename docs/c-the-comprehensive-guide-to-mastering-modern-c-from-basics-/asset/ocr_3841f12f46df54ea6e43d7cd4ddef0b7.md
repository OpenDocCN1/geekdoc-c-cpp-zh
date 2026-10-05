# What Cannot Be Partially Specialized?

In contrast to a class template, it is not possible to partially specialize a function template. A method of a class template also cannot be partially specialized; it must be fully specialized.

# Fully Specialize Class Template

If none of the template arguments for class templates seem to fit, you can also create a full specialization of the class template. In the previous example, I mentioned MyPair<std::string, std::string>. You can implement a full specialization as follows:

```
// https://godbolt.org/z/baPeoTM8
// full specialization
class MyPair<std::string, std::string> {
    std::vector<std::string> data;
public:
    MyPair(const std::string& t, const std::string& u) : data{t, u} {}
};
int main() {
    // uses the full specialization:
    MyPair<std::string, std::string> strStr("c", "d");
}
```

To fully specialize a class template, the angle brackets <> remain empty, as with function templates. The data type or types for which the class template is now to be specialized must be written in the angle brackets after the class name, as seen here in MyPair<string, string>. Through the full specialization of the class template MyPair by MyPair<string, string>, the