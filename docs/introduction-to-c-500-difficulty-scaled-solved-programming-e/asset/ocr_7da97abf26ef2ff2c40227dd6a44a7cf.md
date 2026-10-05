# 370 Introduction to C++

As with arrays, any unassigned member is given the value 0. For example, with the declaration:

the values of year and price members are set to 0.
If the {} are empty, the members are initialized with the default values of their types. For example, with the declaration:

```
Book b = {};
```

the value of b.title becomes "" and the values of b.year and b.price equal to 0.
A structure with automatic storage duration can be initialized by assignment. For example:

```
Book b2 = b1;
```

Note that the initializer (i.e., b1) can be any expression of the proper type. For example, we could replace b1 with a function that returns a structure of Book or *p, where p is a pointer to a structure of that type. Alternatively, we can write Book b2(b1); We will discuss operations on structures in a short.
Finally, a structure variable declared in the variable_list can be initialized at the same time. For example:

```
struct Book {
  string title;
  int year;
  float price;
} b = {\Literature", 2016, 10.85};
```

Since C++II will skip the need to specify the initial value. For example:

```
Book b2(); /* {\Literature", 2016, 10.85};
/* The structure members are initialized with the default values according to their types, that is, the numeric members with 0 and the title with "". */
```

# Pointer to a Structure Member

A pointer to a structure member is used like an ordinary pointer. For example, the following code pointers to display the values of the b members:

```
int main() {
  string *p1;
  int *p2;
  float *p3;
  Book b = {\Literature", 2016, 10.8};

  p1 = &b.title;
  p2 = &b.year;
  p3 = &b.price;

  cout << *p1 << ' ' << *p2 << ' ' << *p3 << ' \\n';
  return 0;
}
```