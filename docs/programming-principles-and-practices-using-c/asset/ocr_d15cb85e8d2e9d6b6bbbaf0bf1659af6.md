We used **static** to get a variable (**dd**) that is created only once, rather than each time `default_date()` is called, and initialized the first time `default_date()` is called. Given `default_date()`, it is trivial to define a default constructor for **Date**:

```
```
Date::Date()
    :y(default_date().year()),
    m(default_date().month()),
    d(default_date().day())
{
}
```
```

Note that the default constructor does not need to check its value; the constructor for `default_date` already did that. Given this default **Date** constructor, we can now define nonempty vectors of **Dates** without listing element values:

```
```
vector<Date> birthdays(10); // ten elements with the default Date value,
                            // Date{}
```
```

Without the default constructor, we would have had to be explicit:

```
```
vector<Date> birthdays(10,default_date()); // ten default Dates

vector<Date> birthdays2 = { // ten default Dates
    default_date(), default_date(), default_date(), default_date(), default_date(),
    default_date(), default_date(), default_date(), default_date(), default_date()
};
```
```

We use parentheses, `()`, when specifying the element counts for a **vector**, rather than the `{}` initializer-list notation, to avoid confusion in the case of a **vector**<**int**> (§18.2).

# ## 9.7.4 const member functions

Some variables are meant to be changed — that’s why we call them “variables” — but some are not; that is, we have “variables” representing immutable values. Those, we typically call *constants* or just **consts**. Consider:

```
```
void some_function(Date& d, const Date& start_of_term)
{
    int a = d.day();   // OK
    int b = start_of_term.day(); // should be OK (why?)
```
```