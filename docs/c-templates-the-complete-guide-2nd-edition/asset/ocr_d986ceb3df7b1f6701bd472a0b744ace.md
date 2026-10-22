not be caught so easily. The following invalid C++ example consists of two files and compiles and links on many implementations, but it is invalid and dangerous: [Click here to view code image](#)

```
```cpp
// Translation unit 1:
template<typename T>
class Danger {
public:
  enum { max = 10 };
};
char buffer[Danger<void>::max]; // uses generic value

extern void clear(char*);

int main()
{
  clear(buffer);
}

// Translation unit 2:
template<typename T>
class Danger;

template<>
class Danger<void> {
public:
  enum { max = 100 };
};

void clear(char* buf)
{
  // mismatch in array bound:
  for (int k = 0; k<Danger<void>::max; ++k) {
    buf[k] = '\0';
  }
}
```
```

This example is clearly contrived to keep it short, but it illustrates that care must be taken to ensure that the declaration of the specialization is visible to all the users of the generic template. In practical terms, this means that a declaration of the specialization should normally follow the declaration of the template in its header file. When the generic implementation comes from an external source (such that the corresponding header files should not be modified), this is not necessarily practical, but it may be worth creating a header including the generic template followed by declarations of the specializations to avoid these hard-to-find errors. We find that, in general, it is better to avoid specializing templates coming from an external source unless it is clearly marked as being designed for that purpose.