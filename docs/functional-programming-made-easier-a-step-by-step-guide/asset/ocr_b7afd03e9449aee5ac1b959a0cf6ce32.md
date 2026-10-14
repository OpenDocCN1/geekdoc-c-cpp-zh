```
log $ show $ parse' yearFirst "1999-12-31" -- COMPILER ERROR!! ①
```

① Once it compiles, it should print (Right (Tuple "" { day: (Day 31), format: YearFirst, month: (Month 12), year: (Year 1999) })). Just a point of interest, the fields are printed in alpha order.

And, of course, we have a compiler error:

![](bbox=[0.233, 0.225, 0.764, 0.44])

Well, from this, it’s clear that we’re missing a Show Instance for Year. Please remedy this and add one for Month, Day and DateFormat while your at it.

Stop reading here and return when the compiler error is gone or you run into issues and need help.

Here are the changes to make the date Types showable: