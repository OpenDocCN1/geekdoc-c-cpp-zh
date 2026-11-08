# No “using” in the Header

As I mentioned at the beginning of the book, for the sake of brevity, I do not use using quite as you should in practice. In Figure 12.2, you can see it done correctly:

+   - Do not use global using in a header.
+   - In a *.cpp file, you can use `using std::identifier`.
+   - However, you should not use `using namespace std;` globally, not even in the *.cpp file.

# 12.8  Initialization via Constructor

You are already familiar with the simple struct Person:

```
struct Person { string name_; int age_; string city_; };
```

You also know that you can initialize the aggregate Person with its three elements in four correct ways:

```
Person p1 { name, age, city };
Person p2 { name, age };
Person p3 { name };
Person p4 { };
```

Now, if we add the *designated initializers* introduced in C++20, there are seven more possibilities:

```
Person p1 { .name_=name, .age_=age, .city_=city };
Person p2 { .name_=name, .city_=city };            // and 2 more
Person p3 { .age_=age };                           // and 2 more
```

All these variants are valid and initialize all fields. The ones not listed are value-initialized, meaning they are filled with a meaningful, usually null-like value or by a default constructor. But what do you do if you want to enforce that a city_ is always specified during initialization? Or if you want to offer the possibility to omit name_ instead of city_ without having to specify the designated initializer?

For this purpose, there are constructors. A *constructor* is a special method of the structure, one specifically designed to initialize the object. You write a constructor *almost* like a normal method, with the following differences: