This gives the output:

```
aa
bb
cc
dd
ee
ff
```

The −1 option basically inverts the strategy for reporting matches by representing each character sequence that does not match as a sub_match. This is often referred to as token splitting (that is, splitting a character stream into tokens) because when your pattern matches the token separators, option−1 leaves you with the tokens. For example:

```
void test2()
{
string s {"1,2 , 3 ,4,5, 6 7"}; // input
regex pat {R"(\s*,\s*)"}; // use comma as token separator copy(sregex_token_iterator{s.begin(),s.end(),pat,-1},
sregex_token_iterator{},
ostream_iterator<string>{cout,"\n"});
}
```

The output is:

```
1
2
3
4
5
67
```

This could equivalently be written using an explicit loop:

```
void test3()
{
sregex_token_iterator end{};
for (sregex_token_iterator p {s.begin(),s.end(),pat,-1}; p!=end; ++p) cout << *p << '\n';
}
```

# 37.5 regex_traits

A regex_traits<T> represents the correspondence between a character type, a string type, and a locale as needed for a regex implementer:

```
template<class C>
struct regex_traits {
public:
using char_type = C;
```