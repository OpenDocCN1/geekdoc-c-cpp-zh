depends on the representation of a **Date**, so I implemented **is_valid()** in terms of a helper function:

```
bool Date::is_valid()
{
return is_date(d,m,y);
}
```

Why have both **is_valid()** and **is_date()**? In this simple example, we could manage with just one, but I can imagine systems where **is_date()** (as here) checks that a **(d,m,y)**-tuple represents a valid date and where **is_valid()** does an additional check on whether that date can be reasonably represented. For example, **is_valid()** might reject dates from before the modern calendar became commonly used.

As is common for such simple concrete types, the definitions of **Date**’s member functions vary between the trivial and the not-too-complicated. For example:

```
inline int Date::day() const
{
return d;
```

```
Date& Date::add_month(int n) {
if (n==0) return *this;

if (n>0) {
int delta_y = n/12; // number of whole years int mm = static_cast<int>(m)+n%12; // number of months ahead if (12 < mm) { // note: dec is represented by12
++delta_y;
mm -= 12;
}
// … handle the cases where the month mm doesn’t have day…

y += delta_y;
m = static_cast<Month>(mm); return *this;
}
// … handle negative n…
return *this;
}
```

I wouldn’t call the code for **add_month()** pretty. In fact, if I added all the details, it might even approach the complexity of relatively simple real-world code. This points to a problem: adding a month is conceptually simple, so why is our code getting complicated? In this case, the reason is that the **d,m,y** representation isn’t as convenient for the computer as it is for us. A better representation (for many purposes) would be simply a number of days since a defined “day zero” (e.g., January 1, 1970). That would make computation on **Dates** simple at the expense of complexity in providing output fit for humans.

Note that assignment and copy initialization are provided by default (§16.2.2). Also, **Date**