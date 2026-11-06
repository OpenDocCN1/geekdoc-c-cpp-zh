# 23.2. THE FORK SYSTEM CALL

```
```cpp
public:
    Find(int nr);
    bool operator() (MapIntChild::value_type &vt) const;
};

Selector    d_selector;
int         d_nr;
MapIntChild d_child;

static void (Monitor::*s_handler[])(int, std::string const &);
static int s_initialize;

public:
    enum Done
    {};

    Monitor();
    void run();

private:
    static void killChild(MapIntChild::value_type it);
    static int initialize();

    Commands    next(int *value, std::string *line);
    void    processInput();
    void    processChild(int fd);

    void    createNewChild(int, std::string const &);
    void    exiting(int = 0, std::string const &msg = std::string());
    void    sendChild(int value, std::string const &line);
    void    stopChild(int value, std::string const &);
    void    unknown(int, std::string const &);
};
```
```

Since there’s only one non-class type data member, the class’s constructor is a very simple function which could be implemented inline:

```
```cpp
inline Monitor::Monitor()
:
    d_nr(0)
{}
```
```

# 23.2.7.4   The class ‘Monitor’: s_handler

The array s_handler, storing pointers to functions needs to be initialized as well. This can be accomplished in several ways:

+   - Since the Commands enumeration only specifies a fairly limited set of commands, compile-time initialization could be considered:

```
```cpp
void (Monitor::*Monitor::s_handler[])(int, string const &) =
{
    &Monitor::unknown,          // order follows enum Command’s
    &Monitor::createNewChild,   // elements
    &Monitor::exiting,
    &Monitor::stopChild,
    &Monitor::sendChild,
};
```
```