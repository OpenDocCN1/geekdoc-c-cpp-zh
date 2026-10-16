```
{
if (y == 0) y = default_date().year();
if (m == Month{}) m = default_date().month(); if (d == 0) d = default_date().day();
if (!is_valid()) throw Bad_date();
}
```

The constructor checks that the data supplied denotes a valid Date. If not, say, for {30,Month::feb,1994}, it throws an exception (§2.4.3.1, Chapter 13), which indicates that something went wrong. If the data supplied is acceptable, the obvious initialization is done. Initialization is a relatively complicated operation because it involves data validation. This is fairly typical. On the other hand, once a Date has been created, it can be used and copied without further checking. In other words, the constructor establishes the invariant for the class (in this case, that it denotes a valid date). Other member functions can rely on that invariant and must maintain it. This design technique can simplify code immensely (see §2.4.3.2, §13.4).

I’m using the value Month{} – which doesn’t represent a month and has the integer value 0–to represent “pick the default month.” I could have defined an enumerator in Month specifically to represent that. But I decided that it was better to use an obviously anomalous value to represent “pick the default month” rather than give the appearance that there were 13 months in a year. Note that Month{}, meaning 0, can be used because it is within the range guaranteed for the enumeration Month (§8.4).

I use the member initializer syntax (§17.4) to initialize the members. After that, I check for 0 and modify the values as needed. This clearly does not provide optimal performance in the (hopefully rare) case of an error, but the use of member initializers leaves the structure of the code obvious. This makes the style less error-prone and easier to maintain than alternatives. Had I aimed at optimal performance, I would have used three separate constructors rather than a single constructor with default arguments.

I considered making the validation function is_valid() public. However, I found the resulting user code more complicated and less robust than code relying on catching the exception:

```
void fill(vector<Date>& aa)
{
while (cin) { Date d; try {
cin >> d;
}
catch (Date::Bad_date) {
// ... myerror handling ...
continue;
}
aa.push_back(d); // see §4.4.2
}
}
```

However, checking that a {d,m,y} set of values is a valid date is not a computation that