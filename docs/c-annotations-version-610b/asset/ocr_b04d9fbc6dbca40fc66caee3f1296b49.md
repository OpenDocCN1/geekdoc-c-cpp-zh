So far for the theory. On some systems the 'out of memory' condition may actually never be reached, as the operating system may interfere before the run-time support system gets a chance to stop the program (see also this link²).

The standard C functions allocating memory (like strdup, malloc, realloc etc.) do not trigger the new handler when memory allocation fails and should be avoided in C++ programs.

# ## 9.3 The assignment operator

In C++ struct and class type objects can be directly assigned new values in the same way as this is possible in C. The default action of such an assignment for non-class type data members is a straight byte-by-byte copy from one data member to another. For now we'll use the following simple class `Person`:

```
```cpp
class Person
{
    char *d_name;
    char *d_address;
    char *d_phone;

public:
    Person();
    Person(char const *name, char const *addr, char const *phone);
    ~Person();
private:
    char *strdupnew(char const *src);   // returns a copy of src.
};

// strdupnew is easily implemented, here is its inline implementation:
inline char *Person::strdupnew(char const *src)
{
    return strcpy(new char [strlen(src) + 1], src);
}
```
```

`Person`'s data members are initialized to zeroes or to copies of the ASCII-Z strings passed to `Person`'s constructor, using some variant of `strdup`. The allocated memory is eventually returned by `Person`'s destructor.

Now consider the consequences of using `Person` objects in the following example:

```
```cpp
void tmpPerson(Person const &person)
{
    Person tmp;
    tmp = person;
}
```
```

Here's what happens when `tmpPerson` is called:

+   - it expects a reference to a `Person` as its parameter `person`.
+   - it defines a local object `tmp`, whose data members are initialized to zeroes.
+   - the object referenced by `person` is copied to `tmp`: `sizeof(Person)` number of bytes are copied from `person` to `tmp`.