```
R> mydata[myData$sex="M",c("person","age","funny","age.mon")
person age funny age.mon
1 Peter 42 High 504
4 Chris 14 Med 168
5 Stevie 1 High 12
6 Brian 7 Med 84
```

The logical conditions you use to subset a data frame can be as simple or as complicated as you need them to. The logical flag vector you in the square brackets has to match the number of records in the data frame. Let's extract the full records for individuals who are more than 10 years old OR have a degree of fitness.

```
R> mydata[myData>10] mydata$funny="High"]
person age funny age.mon
1 Peter 42 High 504
2 Lois 40 F 480
3 Meg 17 F 204
4 Chris 14 M 168
5 Stevie 1 M 12
```

Sometimes, asking for a subset will yield no records. In this case, R returns a data frame with zero rows, which looks like this:

```
R> mydata[age>45]
[1] person age sex funny age.mon
<0 rows (or 0-length row.names)
```

In this example, no records returned from mydata because there are no individuals older than 45. To check whether a subset will contain any records, you can use nrow on the result—if this is equal to zero, then no records have satisfied the specified condition(s).

# Exercise 5.2

a. Create and store this data frame as dfame in your R workspace:

| person | sex | funny |
|---|---|---|
| Stan | M | High |
| Francine | F | Med |
| Steve | M | Low |
| Roger | M | High |
| Hayley | F | Med |
| Klaus | M | Med |