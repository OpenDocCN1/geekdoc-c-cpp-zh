
(c) (defrule example-3
   (not (fact ?x))
   (fact ?y:(< ?y ?x)))
=>
(d) (defrule example-4
   (not (fact ?x))
   (fact ?x:(> ?x 4)))
=>

### 8.21 Rewrite the Blocks World program from Section 7.23 so it can rearrange the blocks from any initial state of stacked blocks to any goal state of stacked blocks. For example, if the initial state of the blocks was:

```
(stack A B C)
(stack D E F)
```

One possible goal state might be:

```
(stack D C B)
(stack A)
(stack F E)
```

### 8.22 Write a CLIPS program that will query a user for color values and then print a list of all countries with flags that contain all of the specified colors. The flag colors for various countries are listed below:

| Country | Flag Colors |
| :--- | :--- |
| United States | Red, white, and blue |
| Belgium | Black, yellow, and red |
| Poland | White and red |
| Monaco | White and red |
| Sweden | Yellow and blue |
| Panama | Red, white, and blue |
| Jamaica | Black, yellow, and green |
| Colombia | Yellow, blue, and red |
| Italy | Green, white, and red |
| Ireland | Green, white, and orange |
| Greece | Blue and white |
| Botswana | Blue, white, and black |

### 8.23 Given the following deftemplate describing a set,

```
(deftemplate set
(multislot name)
(multislot members))
```

write one or more rules that will:

- (a) Compute the union of two specified sets given a fact using the following deftemplate:

```
(deftemplate union
(multislot set-1-name)
(multislot set-2-name))
```

- (b) Compute the intersection of two specified sets given a fact using the following deftemplate:

```
(deftemplate intersection
(multislot set-1-name)
(multislot set-2-name))
```

Note that when computing the union and intersection of the sets, the final result for both (a) and (b) should be a new set fact containing the union or intersection of the two specified sets and the union and intersection facts should be retracted when the operations are complete.

### 8.24 Write a set of rules for classifying syllogistic forms by mood and figure. For example, the syllogism form:

```
No M is P
Some M is not P
.. Some S is P
```

is type EOI-3. The input for the rules should be a single fact representing the major and minor premises and the conclusion. The output should be a printed statement of the mood and figure.

### 8.25 Write a program that will read a data file containing a list of people's names and ages and create a new file containing the list sorted in ascending order by age. The program should prompt for both input and output files. For example, input file:

```
- Linda A. Martin 43
- Phyllis Sebesta 40
- Robert Delwood 38
- Jack Kennedy 39
- Glen Steele 37
```

should create the output file:

```
- Glen Steele 37
- Robert Delwood 38
- Jack Kennedy 39
- Phyllis Sebesta 40
- Linda A. Martin 43
```

### 8.26 Write a program to compute the value of the 13 cards in a bridge player's hand using the point-count method. Aces count for four points; kings count for three points; queens count for two points; and jacks count for one point. A void suit (no cards of one suit) counts for three points; a singleton suit (one card of a suit) counts for two points; and a doubleton suit (two cards of a suit) counts for one point.

### 8.27 Write a program that will indicate the action to be taken when someone swallows poison. The program should have knowledge of the following poisons: acids (such as rust remover and iodine), alkalines (such as ammonia and bleach), and petroleum products (such as gasoline and turpentine). All other poisons should be grouped into the category of other.

In the event of poisoning, a physician or poison control center should be called. For acids, alkalines, and other types of poison (but not petroleum products), dilute the poison by having the victim drink a liquid such as water or milk. Induce vomiting for other types of poison, but do not induce vomiting for acids, alkalines, or petroleum products. Do not give liquids or induce vomiting if the victim is unconscious or is having convulsions.

### 8.28 Write a program that, when given two points, computes the slope of the line formed by the two points. Your program should check to ensure that the points provided contain numbers and that one point is not specified twice: Treat vertical lines as having an infinite slope.

### 8.29 A scalene triangle has three unequal sides. An isosceles triangle has two sides of the same length. An equilateral triangle has three sides of the same length. Write a program that, when given the three points forming a triangle, will determine the type of triangle. The program should account for possible round-off error (assume two sides are equal if the difference between their lengths is less than .00001). Test your program with the following triangles:

- (a) Points (0,0), (2,4), and (6,0).
- (b) Points (1,2), (4,5), and (7,2).
- (c) Points (0,0), (-3.5, 1.96152), and (6,0).

### 8.30 Write a program to solve the Towers of Hanoi problem in which you must move a set of rings from one peg to another peg without ever putting a larger ring on top of a smaller ring. There are three pegs for you to use. The number of rings should be an input to the program. In the initial configuration all the rings are on the first peg in descending size from bottom to top. The initial goal should be to move all of the rings from the first peg to the third peg.

### 8.31 Write a program to determine the values of the letters that make the following crypt-arithmetic problem correct. Each of the letters H, O, C, U, S, P, R, E, and T corresponds uniquely to a digit in the range 0 to 9.

```
HOCUS
+ FOCUS
= PRESTO
```

### 8.32 Write a program that gives advice on investing in mutual funds. The output of the program should indicate the percentage of money to be invested in fixed-income funds; funds mainly investing in bonds and preferred stocks; and stock funds, funds with higher risk but greater potential returns. The percentage will be determined by 'scoring' each of a number of questions and then taking the average responses to various questions. If the investor is 29 years old or younger, add 4 to the score; 30 to 39, add 3; 40 to 49, add 2; 50 to 59, add 1; and 60 or more, add 0. If the investor has 0 to 9 years until retirement, add 0; 10 to 14, add 1; 15 to 19, add 2; 20 to 24, add 3; and 25 or more, add 4. If the investor is willing to ride out losses of only 5% or less, add 0 to the score; 6% to 10%, add 1; 11% to 15%, add 2; and 16% or more, add 3. If the investor is very knowledgeable about investments and the stock market, add 4 to the score; if somewhat knowledgeable, add 2; and if not very knowledgeable, add 0 to the score. If the investor is willing to take significant risk for higher possible returns, add 4 to the score; if some risk, add 2; and if little risk, add 0. If the investor believes his or her retirement will be met given his or her current income and assets, add 4 to the score; if the goals might possibly be met, add 2; if the goals are unlikely to be met, add 0. If the final score is more than 20 points, then 100% of the investments should be in stock funds; if 16 to 20 points, 80% should be in stock funds and 20% in fixed-income funds; if 11 to 15 points, 60% should be in stock funds and 40% in fixed-income funds; if 6 to 10 points, then 40% should be in stock funds and 60% in fixed-income funds; if 0 to 5 points, then 20% should be in stock funds and 80% in fixed-income funds.

### 8.33 Modify the program developed for Problem 7.12 on page 362 so that the information about stars is represented using facts. The program output should be the same order: all stars having the specified spectral class, all stars having the specified magnitude, and finally all stars matching both the spectral class and magnitude along with their distance from Earth in light-years.

## CHAPTER 9
Modular Design, Execution Control, and Rule Efficiency

### 9.1 INTRODUCTION

This chapter introduces a number of CLIPS features useful for the development and maintenance of expert systems. Deftemplate attributes allow the enforcement of value constraints for deftemplate slot values. When a rule is loaded, deftemplate constraint attributes can detect semantic errors that prevent the LHS of that rule from being matched. Using salience, which provides a method for prioritizing rules, and facts representing flow of control knowledge, this chapter demonstrates techniques for controlling the execution of a CLIPS program. In addition, it looks at the deffmodule construct, which allows a knowledge base to be partitioned and provides a more explicit method for controlling the execution of a system. This chapter also provides many techniques for increasing the efficiency of a rule-based expert system that uses the Rete Pattern Matching algorithm. The reasons for needing an efficient pattern-matching algorithm will be discussed before the Rete algorithm is explained. Several techniques for writing rules more efficiently will also be discussed.

### 9.2 DEFTEMPLATE ATTRIBUTES

CLIPS provides a number of slot attributes that can be specified when a deftemplate's slots are defined. These attributes aid in the development and maintenance of an expert system by providing strong typing and constraint checking. It is possible to define the allowed types and values that can be stored in a slot. For numeric values, the allowed range of numbers can be specified. Multislots can specify the minimum and maximum number of fields they can contain. Finally, the default attribute provides a default slot value to be used for slots that are not specified in an assert command.
