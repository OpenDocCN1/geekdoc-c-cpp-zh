the raw frequencies themselves are usually displayed, a barplot can also be used to visualize other quantities, such as means or proportions, which directly depend upon these frequencies.

As an example, let's use the mtcars data set from Exercise 13.4 (b) on page 287. Detailing various characteristics of 32 classic performance cars in the mid-1970s, the first five records can be viewed directly from the prompt.

```
mtcars[1:5]
mmg disp hp drat wt vs am gear carb
Mazda RX4 21.0 6 160 110.3 2.620 16.46 0 1 4
Mazda RX4 Wag 21.0 6 160 110.3 2.875 17.02 0 1 4
Datsun 710 22.8 4 108 93 2.320 18.61 1 1 4
Hornet 4 Drive 21.4 6 258 110.3 3.215 19.44 1 0 3
Hornet Sportabout 18.7 8 360 175.3 3.445 17.02 0 0 2
```

The documentation in mtcars explains the variables that have been recorded. Of these, cyl provides the number of cylinders in each engine—four, five, six, or eight. To find out how many cylinders were observed with each number of cylinders, you can use table, as shown here:

```
cyl.freq <- table(mtcars$cyl)
cyl.freq
4 6 8
11 7 14
```

The result is easily displayed as a barplot, as shown here:

```
barplot(cyl.freq)
```

You can find the resulting barplot on the left of Figure 14-1.

![](bbox=[0.238, 0.642, 0.837, 0.843])

Figure 14-1: Two examples of data from mtcars using base R graphics. Left: The simplest, default version, using one categorical variable. Right: A "dodged" barplot illustrating various visual options and using two categorical variables.