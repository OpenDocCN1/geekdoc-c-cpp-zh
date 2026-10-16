```
public:
Date(int dd =0, int mm =0, int yy =0);
// ...
static void set_default(int dd, int mm, int yy); // set default_date to Date(dd,mm,yy)
};
```

We can now define the Date constructor to use default_date like this:

```
Date::Date(int dd, int mm, int yy)
{
d=dd?dd:default_date.d; m = mm ? mm : default_date.m; y = yy ? yy : default_date.y;
// ... checkthat the Date is valid ...
```

Using set_default(), we can change the default date when appropriate. A static member can be referred to like any other member. In addition, a static member can be referred to without mentioning an object. Instead, its name is qualified by the name of its class. For example:

```
void f()
{
Date::set_default(4,5,1945); // call Date's static member set_default()
}
```

If used, a static member – a function or data member – must be defined somewhere. The keyword static is not repeated in the definition of a static member. For example:

```
Date Date::default_date {16,12,1770}; // definition of Date::default_date
void Date::set_default(int d, int m, int y)
{
default_date = {d,m,y};
}
// definition of Date::set_default
// assign newvalue to default_date
```

Now, the default value is Beethoven’s birth date – until someone decides otherwise. Note that Date{} serves as a notation for the value of Date::default_date. For example:

```
Date copy_of_default_date = Date{};
void f(Date);
void g()
{
f(Date{});
}
```

Consequently, we don’t need a separate function for reading the default date. Furthermore, where the target type is unambiguously a Date, plain {} is sufficient. For example: