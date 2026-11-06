```
```
(using first)
3
(using second)
4.5
(using first)
10.5
```
```

From the middle two lines you can see that the computer did indeed call the second version of the template.

You can make life a little easier by using a little trick. Most compilers let you leave out the type in angle brackets in the function template call itself. The compiler is smart enough to figure out what type of function to build from the template, based on the types that you pass into the function call! Pretty wild. Here's an example main() that you can substitute for the main() in Listing 5-9:

```
```cpp
int main()
{
    int n = -3;
    cout << AbsoluteValue(n) << endl;

    float *ptr = new float(-4.5);
    cout << AbsoluteValue(ptr) << endl;
    cout << AbsoluteValue(10.5) << endl;

    return 0;
}
```
```

In this code, we replaced AbsoluteValue<int>(n) with just AbsoluteValue(n). When you run the modified Listing 5-9, you see the same output as when you run Listing 5-9.

# ## Templatizing a member function

When you write a template for a class, you can put function templates inside the class template. To people who were familiar with some of the early versions of C++ where template support was minimal, this seems a little shocking. But when the electrical current wears off, we all see that putting a template function inside a template class is possible. You simply declare a function template inside a class, as in the following:

```
```cpp
class MyMath
{
public:
    string name;

    MyMath(string aname) : name(aname) {}

    template <typename T> void WriteAbsoluteValue(T x)
    {
        cout << "Hello " << name << endl;
        if (x >= 0)
```
```