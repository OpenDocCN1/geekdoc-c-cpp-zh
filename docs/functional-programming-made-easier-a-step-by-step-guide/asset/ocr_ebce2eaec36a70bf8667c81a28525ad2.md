And finally, we’ll need 2 `Parsers`. One to handle each format we’re supporting.

That seems to be all that we’ll need to accomplish our goal of date parsing. So let’s get started.

First thing to do is model the Type. Please code up a Type that will model the parsed date before reading on.

Modeling is always difficult because there are always so many ways to do it. Our goal should be to find the best model for our situation. That’s difficult to do in the real world but even more so in an artificial environment that we work in when we’re learning.

So, I’m going to through a few possibilities and then I’m going to pick one based on totally artificial criteria.

Here’s the most naïve approach:

```
data DateParts = DateParts Int Int Int
```

Looking at the 3 `Ints` it’s impossible to tell which is year and which is day or month. Let’s fix that:

```
newtype Year = Year Int
newtype Month = Month Int
newtype Day = Day Int

data DateParts = DateParts Year Month Day
```

Keep in mind that these are the parts that we parsed out of a `String`. This is not guaranteed to be a valid date. That’s beyond the scope of this problem. In the real world, we’d first parse the date and then use a date library to do the hard work of validation for us.

Can you see any improvements that we could make on model? I can only see one.

It might be nice to know what format we originally encountered when we parsed the date just in case we want to print it back out in it’s original format.

We’ll create a Sum Type for that:

```
data DateParts
  = YearFirstDate Year Month Day
  | MonthFirstDate Year Month Day
```

Now, that we’ve done that, let’s start over but take a different tact. We’ll start with: