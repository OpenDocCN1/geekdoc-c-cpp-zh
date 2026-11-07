# # Visualization with raylib—Law of Large Numbers Animation

10.21 (Law of Large Numbers Animation) In Sections 5.10 and 6.4.7, we used random-number generation to simulate the roll of a six-sided die. In this next raylib case study exercise, you’ll use dynamic visualization to make the Law of Large Numbers⁷,⁸ “come alive” in a die-rolling simulation that displays an animated bar chart. As the simulation repeatedly rolls the die, it updates an array of the frequencies with which each face appears. Then, it displays each die face’s frequency, its percentage of the total rolls and a bar whose length represents the frequency’s magnitude.

For a six-sided die, the face values 1 through 6 each should occur with “equal likelihood”—the probability of each face appearing on any roll is 1/6th or approximately 16.67%. If we roll a die 6000 times, we’d expect about 1000 of each face to appear. Like coin tossing, die rolling is random, so faces could occur fewer or more than 1000 times. As the number of die rolls increases, the Law of Large Numbers says that each of the frequencies should approach the expected value of 16.67%. If so, the bars in the bar chart should become nearly identical in length, as shown in the following screen captures of three sample executions for 60, 6000 and 6,000,0000 dice:

![](bbox=[0.255, 0.42, 0.745, 0.65])

> > 7. “Law of large numbers.” Accessed December 18, 2020. https://encyclopediaofmath.org/index.php?title=Law_of_large_numbers.

> > 8. “Law of large numbers.” Accessed December 18, 2020. https://en.wikipedia.org/wiki/Law_of_large_numbers.