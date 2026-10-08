```
Date next_weekday(const Date& d) { /* . . . */ }
```

```
bool leapyear(int y) { /* . . . */ }
```

```
bool operator==(const Date& a, const Date& b) {
    return a.year()==b.year()
        && a.month()==b.month()
        && a.day()==b.day();
}
```

```
bool operator!=(const Date& a, const Date& b) {
    return !(a==b);
}
```

Helper functions are also called *convenience functions*, *auxiliary functions*, and many other things. The distinction between these functions and other nonmember functions is logical; that is, “helper function” is a design concept, not a programming language concept. The helper functions often take arguments of the classes that they are helpers of. There are exceptions, though; note **leapyear**(). Often, we use namespaces to identify a group of helper functions; see §8.7:

```
namespace Chrono {
    enum class Month { /* . . . */ };
    class Date { /* . . . */ };
    bool is_date(int y, Month m, int d);         // true for valid date
    Date next_Sunday(const Date& d) { /* . . . */ }
    Date next_weekday(const Date& d) { /* . . . */ }
    bool leapyear(int y) { /* . . . */ }            // see exercise 10
    bool operator==(const Date& a, const Date& b) { /* . . . */ }
    // . . . 
}
```

Note the **==** and **!=** are functions. They are typical helpers. For many classes, **==** and **!=** make obvious sense, but since they don’t make sense for all classes, the compiler can’t write them for you the way it writes the copy constructor and copy assignment.

Note also that we introduced a helper function **is_date**(). That function replaces **Date::is_valid**() because checking whether a date is valid is largely independent of the representation of a **Date**. For example, we don’t need to know how **Date** objects are represented to know that “January 30, 2008” is a valid date and “February 30, 2008” is not. There still may be aspects of a date that depend on