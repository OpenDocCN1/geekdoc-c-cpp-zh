for things like colors, shapes, and fruits. Magnitude comparisons will not make sense with these and they will not work if you try to use them.

# Equality vs. Identity (Advanced)

If you have experience with Java, you might find the behavior of == confusing. This is because in Scala, == does what most people expect, it checks for equality between values. For anyone who has not programmed in Java he/she might wonder what other options there are. We will see later that objects with the same value are not necessarily the same objects. If you go to a store and pick up two boxes of the same type of item, they are basically equal as far as you can tell, but they are not the same object. Each one has its own identity.

There are times in programming when you don’t want to just check if two things are equal, you want to actually know if they are the same thing. This requires doing a check for identity. In Scala we use eq to check if two things are the same thing. We can show an example of where eq and == return different result.

```
scala> "sssss" eq "s"*5
res8: Boolean = false
```

```
scala> "sssss" == "s"*5
res9: Boolean = true
```

# 4.4 Boolean Logic

Imagine if the theme park had a policy where seniors are charged the same amount as children. So now anyone over 65 or anyone under 13 should pay the reduced rate. We could accomplish this by having separate if statements in either the functional or the imperative manner.

```
val cost = if(age<13) 20 else if(age>65) 20 else 35
```

or

```
var cost=20
if(age>=13) cost=35
if(age>65) cost=20
```

Both of these are verbose, potentially inefficient, and prone to errors. The errors occur because in both we had to enter the number 20 in two places. What we would really like to say is exactly what we said in English. We want to say that we use the lower rate if the person is under 13 or over 65 and use the higher rate otherwise. Boolean logic gives us the ability to say this.

There are four different BOOLEAN OPERATORS we can use to build complex Boolean expressions from simple ones. These are shown in table 4.1. Table 4.2 shows the value that results from applying these different operators on different arguments.