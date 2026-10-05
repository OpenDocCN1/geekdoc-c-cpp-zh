This operator has not been overloaded for the class, the compiler will immediately report an error. Thus, in order to take advantage of the template, the greater than operator must be overloaded for the class.

# 10.3 Class Templates

The need for class templates is similar to the need for function templates. The need for generic classes (Queue, Stack, Array, etc.) that handle data of different types is felt frequently. Let us consider the set of three classes in Listing 10.13 member functions have similar definitions, the mere difference being the type of the private data members upon whom they operate.

Listing 10.13 Classes with similar definition

```
class X_for_int
{
    int val;
    public:
    void f1(const int &);
    void f2(const int &);
    /*
    rest of the class X_for_int
    */
};
class X_for_char
{
    char val;
    public:
    void f1(const char &);
    void f2(const char &);
    /*
    rest of the class X_for_char
    */
};
class X_for_string
{
    string val;
    public:
    void f1(const string &);
    void f2(const string &);
    /*
    rest of the class X_for_string
    */
};
```

The X_for_int, X_for_char, and X_for_string defined in Listing 10.13 are similar in every respect except for the type of their data members. As expected, the presence of three different classes that are different only in the data type of the data members upon whom their member functions work creates huge difficulties in code maintenance. Any change in one of the classes will have to be replicated in all of the others. This situation certainly