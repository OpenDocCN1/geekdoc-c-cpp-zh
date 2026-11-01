# Chapter 2.2

# I.23: Keep the number of function arguments low

# How much should they earn?

Here’s a function declaration:

Click here to view code image

```
double salary(PayGrade grade, int location_id);
```

It’s nice to see “double salary” at the start of a line of code; sadly, the purpose of this function is not to double your salary, but to report a salary for a particular pay grade at a particular location. Also, as remarked earlier, you should use integral types for money, so we shall redeclare this function, thus:

Click here to view code image

```
int salary(PayGrade grade, int location_id);
```

You might see this sort of thing in a government contract: civil servant salaries are often pegged to a pay grade but will vary by location. In the UK, for example, some civil servants in London are paid more because of the increased cost of living in the capital.

This is a perfectly normal, ordinary function. It doesn’t appear to rely on external information and in all likelihood simply queries a database table to retrieve the data. It has the look and feel of a first attempt at a function: simple, unambiguous, quiet, unassuming.

Then one day, by act of parliament or some other great immovable object of irre-sistible progress, the requirements change, and salaries are now calculated based not only on pay grade and location, but also on length