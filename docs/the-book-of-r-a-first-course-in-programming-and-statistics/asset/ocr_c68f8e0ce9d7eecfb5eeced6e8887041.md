If you're ever unsure of the result of your specification, you can use the layout.show function to see how plots will be placed. The following line produces the image on the left of Figure 23-3.

```
layout.show(n=max(lay.mat))
```

Then, once you've loaded the MASS package by calling library("MASS") you can access survey, running the following lines to place the plots in the order the plotting commands are executed, matched to the integers in lay.mat.

```
plot(survey$Wr.Hnd,survey$Height)
xlab="Writing handspan",ylab="Height"
boxplot(survey$Height$Smoke,
xlab="Smoking frequency",ylab="Height"
barplot(table(survey$Exer),horiz=TRUE,main="ExerciseExercise")
```

Note that if you've already closed the plot around layout, then you'll need to reinitialize a new device with the same call to layout for these three plots to display as intended. The result should look like the right of Figure 23-3.

![](bbox=[0.268, 0.447, 0.851, 0.672])

Figure 23-3: Left: layout.show to visualize the planned plotting layout and order. Right: Demonstrating three plots of the survey data arranged according to lay.mat layout.

Probably the biggest benefit of layout is its ability to release the rigidity of plotting cells when compared to using the mflow par option, you've just seen. Additional arguments to layout, namely, widths and heights, even allow you to preset the relative widths and heights of the cells as structured in the mat argument. See the documentation in ?layout for details; you'll find some other examples of its flexibility at the bottom of the file.