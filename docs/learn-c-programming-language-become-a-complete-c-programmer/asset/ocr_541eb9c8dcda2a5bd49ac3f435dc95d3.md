```
```cpp
class Date {
int d, m, y;
public:
Date(int dd =0, int mm =0, int yy =0);
// ...
};

Date::Date(int dd, int mm, int yy) {
d=dd?dd:today.d; m=mm?mm:today.m; y=yy?yy:today.y;
// checkthat the Date is valid
}
```
```

When an argument value is used to indicate “pick the default,” the value chosen must be outside the set of possible values for the argument. For **day** and **month**, this is clearly so, but for **year**, zero may not be an obvious choice. Fortunately, there is no year zero on the European calendar; 1AD (**year==1**) comes immediately after 1BC (**year==-1**).

Alternatively, we could use the default values directly as default arguments:

```
```cpp
class Date {
int d, m, y;
public:
Date(int dd =today.d, int mm =today.m, int yy =today.y);
// ...
};

Date::Date(int dd, int mm, int yy) {
// checkthat the Date is valid
}
```
```

However, I chose to use **0** to avoid building actual values into **Date**’s interface. That way, we have the option to later improve the implementation of the default.

Note that by guaranteeing proper initialization of objects, the constructors greatly simplify the implementation of member functions. Given constructors, other member functions no longer have to deal with the possibility of uninitialized data (§16.3.1).

# 16.2.6 **explicit** Constructors

By default, a constructor invoked by a single argument acts as an implicit conversion from its argument type to its type. For example:

```
```cpp
complex<double> d {1}; // d == {1,0} (§5.6.2)
```
```

Such implicit conversions can be extremely useful. Complex numbers are an example: if we leave out the imaginary part, we get a complex number on the real axis. That’s exactly what mathematics requires. However, in many cases, such conversions can be a significant source of confusion and errors. Consider **Date**:

```
```cpp
void my_fct(Date d);
```
```