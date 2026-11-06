# 18.5 Classes having pointer data members (C++11)

Classes having pointer data members require special attention. In particular at construction time one must be careful to prevent wild pointers and/or memory leaks. Consider the following class defining two pointer data members:

```
```cpp
class Filter
{
        istream *d_in;
        ostream *d_out;
    public:
        Filter(char const *in, char const *out);
};
```
```

Assume that Filter objects filter information read from *d_in and write the filtered information to *d_out. Using pointers to streams allows us to have them point at any kind of stream like isstreams, ifstreams, fstreams or istringstreams. The shown constructor could be implemented like this:

```
```cpp
Filter::Filter(char const *in, char const *out)
:
        d_in(new ifstream(in)),
        d_out(new ofstream(out))
{
        if (!*d_in || !*d_out)
                throw string("Input and/or output stream not available");
}
```
```

Of course, the construction could fail. new could throw an exception; the stream constructors could throw exceptions; or the streams could not be opened in which case an exception is thrown from the constructor’s body. Using a function try block helps. Note that if d_in’s initialization throws, there’s nothing to be worried about. The Filter object hasn’t been constructed, its destructor is not called and processing continues at the point where the thrown exception is caught. But Filter’s destructor is also not called when d_out’s initialization or the constructor’s if statement throws: no object, and hence no destructor is called. This may result in memory leaks, as delete isn’t called for d_in and/or d_out. To prevent this, d_in and d_out must first be initialized to 0 and only then the initialization can be performed:

```
```cpp
Filter::Filter(char const *in, char const *out)
try
:
        d_in(0),
        d_out(0)
{
        d_in = new ifstream(in);
        d_out = new ofstream(out);

        if (!*d_in || !*d_out)
                throw string("Input and/or output stream not available");
}
catch (...)
{
        delete d_out;
        delete d_in;
}
```
```

This quickly gets complicated, though. If Filter harbors yet another data member of a class whose constructor needs two streams then that data cannot be constructed or it must itself be converted into a pointer: