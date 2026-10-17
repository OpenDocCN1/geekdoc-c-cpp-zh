
第一个版本使用 `<`，第二个版本使用用户提供的比较 `cmp`。例如，我们可能决定使用不区分大小写的比较来对水果进行排序。我们通过定义一个函数对象（§3.4.3，§19.2.2）在对字符串对调用时进行比较来实现：

```
class Nocase { // case-insensitive string compare

public:

    bool operator()(const string&, const string&) const;

};
```

```
bool Nocase::operator()(const string& x, const string& y) const // return true if x is lexicographically less than y, not taking case into account

{
    auto p = x.begin(); auto q = y.begin();

    while (p!=x.end() && q!=y.end() && toupper(*p)==toupper(*q)) { ++p; ++q; }

    if (p == x.end()) return q != y.end();

    if (q == y.end()) return false;

    return toupper(*p) < toupper(*q);
}
```
