Window Cowboy
WWindow CCowboy
Cowboy_window Had the designer of Window been a bit more careful and specified draw() to be const, the whole problem would have evaporated. I find that fairly typical.

# 21.3.4 Repeated Use of a Base Class

When each class has only one direct base class, the class hierarchy will be a tree, and a class can only occur once in the tree. When a class can have multiple base classes, a class can appear multiple times in the resulting hierarchy. Consider a class providing facilities for storing state in a file (e.g., for breakpointing, debug information, or persistence) and restoring it later:

```
struct Storable { // persistent storage
virtual string get_file() = 0;
virtual void read() = 0;
virtual void write() = 0;

virtual ~Storable() {}
};
```

Such a useful class will naturally be used in several places in a class hierarchy. For example:

```
class Transmitter : public Storable { public:
void write() override;
// ...
};
```

```
class Receiver : public Storable { public:
void write() override;
// ...
};
```

```
class Radio : public Transmitter, public Receiver {
public:
string get_file() override;
void read() override;
void write() override;
// ...
};
```

Given that, we could imagine two cases:

+   [1] A Radio object has two subobjects of class Storable (one for Transmitter and one for Receiver ).
+   [2] A Radio object has one subobject of class Storable (shared by Transmitter and Receiver). The default, provided for the example as written, is two subobjects. Unless you