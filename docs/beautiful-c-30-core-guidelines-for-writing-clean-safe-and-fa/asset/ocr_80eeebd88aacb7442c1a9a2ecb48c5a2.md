class.

+   1. RAII is discussed in Chapter 5.6.

We’ll call the class command_stream. It needs to optionally own a std::istream, so we can start with this:

Click here to view code image

```
class command_stream {
private:
    bool owned;        // Possibly owns the
std::istream
    std::istream* inp;  // Here is the std::istream
};
```

There’s not much in there. The destructor is trivial:

Click here to view code image

```
class command_stream {
public:
    ~command_stream() {
        if (owned) delete inp;
    }

private:
    bool owned;        // Possibly owns the
std::istream
    std::istream* inp;  // Here is the std::istream
};
```

The constructor should take a parameter to indicate which input stream it should be forwarding to, and an optional filename or command. Fortunately, we already have an enumeration we can use, so our class now looks like this:

Click here to view code image