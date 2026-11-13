For example, consider the input “Able were you ere you saw Elba.” This looks like a palindrome until you see the first “e” in “were,” so a suitable output would be

```
That is not a palindrome.
Mismatch discovered at: Able we
```

+   9. How would you modify the palindromes program so that upper- and lowercase versions of letters are considered different? In the modified program the string “able were I ere I saw elba” would still be considered a palindrome, but the string “Able was I ere I saw Elba” would no longer be considered a palindrome, since, among other things, the first and last letters, “A” and “a,” are not the same under these changed rules.

# PROGRAMMING EXAMPLE: Car Wash Simulation

The Handy-Dandy Hand Car Wash Company has decided to modernize and change its image. It has installed a fast, fully automated car-washing mechanism that can wash a car in one to ten minutes. It will soon reopen under its new name The Automatic Autowash Emporium. The company wants to know the most efficient way to use its new car-washing mechanism. If the mechanism is used on the fast setting, it can wash a car in one minute, but because of the high pressure required to operate at such speed, the mechanism uses a great deal of water and soap at this setting. At slower settings, it takes longer to wash a car but uses less soap and water. The company wants to know how many customers will be served and how long customers will have to wait in line when the washing mechanism is used at one of the slower speeds. The company also wants to know whether its new motto, “You Ought to Autowash your Auto,” will be effective. We respectively refuse comment on the motto, but we agree to write a program that will simulate automobiles waiting in line for a car wash. This way the manager of the car wash can see how the speed of the car wash, the length of the line, and various other factors interact.

# Car Wash Simulation—Specification

The precise program specifications are given by the following input/output descriptions:

Input. The program has three input items: (1) the amount of time needed to wash one car (in total seconds); (2) the probability that a new customer arrives during any given second (we assume that, at most, one customer arrives in a second); and (3) the total length of time to be simulated (in seconds).

Output. The program produces two pieces of output information: (1) the number of customers serviced in the simulated time; and (2) the average time that a customer spent in line during the simulation (in seconds).