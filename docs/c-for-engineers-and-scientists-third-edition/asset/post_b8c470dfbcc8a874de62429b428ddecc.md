
# Chapter 1 19

Preliminary Three: Software Development

should tell the user that the data is invalid. Developing good test procedures and data for sophisticated problems can be more difficult than writing the code itself.

Table 1.3 lists the comparative amount of effort that's typically spent on each development and design step in large commercial programming. As this listing shows

Table 1.3 Effort Expended in Phase I
| Step | Effort |
|---|---|
| Analyze the problem | 10% |
| Develop a solution | 20% |
| Code the solution (write the program) | 20% |
| Test the program | 50% |

# Phase II: Documentation

Because of inadequate documentation, so much your work becomes useless or lost and many tasks must be repeated, documentation is one of the most important steps in problem solving. Critical documents are created during the analysis, design, coding, and testing steps. Documentation phase requires collecting these documents, adding user-operating material, and presenting documentation in a form that's most useful to you and your organization.

Although everybody classifies them in the same way, there are five main documents for every problem solution:

- * Program description
- Algorithm development and changes
- Well-commented program listing
- Sample tests
- Users' manual

Putting yourself in the shoes of a person who might use your work—from secretaries to programmers/analysts and management—should you strive to make the content of important documentation clear. The documentation phase formally begins in the development and design phase and continues into the maintenance phase.

# Phase III: Maintenance

This phase is concerned with the ongoing correction of problems, revisions to meet meeting needs, and addition of new features. Maintenance is often the major effort, the primary source of revenue, and the longest lasting of the engineering phases. Development might take days or months, but maintenance could continue for years or decades. The better the documentation is, the more efficiently maintenance can be performed, and the happier customers and end users will be.

# 20 Preliminaries

# Backup

Although not part of the formal design process, making and keeping backup copies of the program at each step of the programming and debugging process are critical. Deleting or changing a program's current working version beyond recognition is all easy. With backup copies, you can recover the last stage of work with little effort. The final version of a useful program should be backed up at least twice. In this regard, another programming proverb is, "Backup is unimportant if you don't starting over again."

Many organizations keep at least one backup on site, where it can be retrieved easily, and another backup copy in a fireproof safe or at a remote location.

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_39_0.png)

# EXERCISES 1.3

**Note:** In each of these exercises, a programming problem is given. Read the problem statement first, and then answer the questions pertaining to the problem. **Do not** attempt to write a program to solve the problems. Simply answer the questions following the programming specifications.

- 1. (Electric Eng.) You have been asked to write a C++ program to calculate the total resistance of a series circuit. The total resistance is the sum of all individual resistance values. The circuit consists of 56-ohm, 33-ohm, and 15-ohm resistors.
  a. For this programming problem, how many outputs are required?
  b. How many inputs does this problem have?
  c. Determine a formula for converting input items into output items. The number of 56-ohm resistors is $m$, the number of 33-ohm resistors is $n$, and the number of 15-ohm resistors is $p$.
  d. Test the formula written for Exercise 1c, using the following sample data: $m = 17$, $n = 24$, and $p = 12$.

- 2. (Physics) You have been asked to write a program to calculate the value of distance, in miles, given this relationship:
distance = rate $\times elapsed time$
  a. For this programming problem, how many outputs are required?
  b. How many inputs does this problem have?
  c. Determine a formula for converting input items into output items.
  d. Test the formula written for Exercise 2c, using the following sample data: $rate$ is 55 miles per hour and $elapsed time$ is 2.5 hours.
  e. How must the formula determined in Exercise 2c be modified if the elapsed time is in minutes instead of hours?

# Chapter 1

# 21

Preliminary Three: Software Development

3. (Electrical Eng.) You've been asked to write a program that outputs the following specifications:
Voltage: 35
Power:
Bandwidth: 15 kHz
  a. For this programming problem, how many outputs are required?
  b. How many inputs does this problem have?
  c. Determine a formula for converting input items into output items.

4. (Physics) You've been asked to write a program to determine how far a car has traveled after 10 seconds, assuming the car is initially traveling at 60 mph and the driver applies the brakes at a uniform rate. Use the following formula: distance = $ut - 0.5at^2$
  a. For this programming problem, how many outputs are required?
  b. How many inputs does this problem have?
  c. Determine a formula for converting input items into output items.
  d. Test the formula written for the problem.

5. (General Math) Consider the following problem: If an amount is deposited in a bank paying 5% interest, compounded annually, what would the balance be at the end of 2 years? The following is required: Balance = $P(1+r)^t$
  a. For this programming problem, how many outputs are required?
  b. How many inputs does this problem have?
  c. Determine a formula for converting input items into output items.
  d. Test the formula written for Exercise 5c, using the data in the problem.

6. (Electrical Eng.) You've been asked to write a program that calculates the sum of two voltages. The voltage for the first circuit is given by this formula: $V_1 = 150V$
The voltage for the second circuit is given by this formula: $V_2 = \sqrt{V^2 + f^2}$
$V$ is the input voltage.
$f$ is the frequency in Hertz.
  a. For this programming problem, how many outputs are required?
  b. How many inputs does this problem have?
  c. Determine a formula for converting input items into output items.
  d. Test the formula written for Exercise 6c, using the following sample data: the first circuit is operated at 144 Hz, and the second circuit is operated at 100 Hz.

7. (Statistics) Consider the following problem: This is the formula for the normal deviate, $z$: $z = (X - \mu)/\sigma$
$X$ is a single value.
$\mu$ refers to an average value.
$\sigma$ refers to standard deviation.
Using this, you need to write a program that calculates the value of $z$ when $X=85$, $\mu = 80$, and $\sigma = 4$.
  a. For this programming problem, how many outputs are required?
  b. How many inputs does this problem have?
  c. Determine a formula for converting input items into output items.
  d. Test the formula written for Exercise 7c, using the data in the problem.

8. (Electrical Eng.) Read the following problem statement: The electrical resistance, $r$, of the metal wire, in ohms, is given by this formula: $r = \frac{ml}{a}$
$m$ is the resistivity of the metal.
$l$ is the length of the wire in feet.
$a$ is the cross-sectional area of the wire in circular mils.
Using this, you need to write a C++ program to calculate the resistance of a wire that's 125 feet long, has a cross-sectional area of 500 circular mils, and is copper. The resistivity of copper, $m_c$, is 10.4.
  a. Determine the outputs required of the program.
  b. What many inputs does the program require?
  c. What is the formula for obtaining the outputs from the inputs?

# 1.4 Preliminary Four: Algorithms

Before a program is written, the programmer must clearly understand what data are to be used, the desired result, and the procedure used to produce this result. As mentioned previously, the procedure, or solution, selected is referred to as an algorithm. More precisely, an algorithm is defined as a step-by-step sequence of instructions that must terminate and describe how the data is to be processed to produce the desired outputs. In essence, an algorithm answers the question “What method will you use to solve this problem?”
