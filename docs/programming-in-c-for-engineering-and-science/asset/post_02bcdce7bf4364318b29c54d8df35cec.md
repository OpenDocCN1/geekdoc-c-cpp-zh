
Assume that R = 15 ft and r = 0.2 ft and that the initial condition is h(0) = 28 ft. Solve this initial-value problem for h, using a step size of Δt = 1 min and continuing the calculations until the water height becomes less than 0.2 ft.

## 31. A new gas well is estimated to contain 9000 tons of natural gas at a pressure of p₀ = 900 psia. The distribution system is connected to the well at the discharge pressure p* = 400 psia. The discharge Q in tons per day through the outlet pipe from the well is approximated by the equation Q = α(p² − p*²)^β, where α = 1.115 × 10⁻⁴, β = 0.8, and p = initial pressure of gas in the well in psia. It is also assumed that the gas pressure is directly proportional to the discharge Q, which is modeled by the differential equation

```
dp/dt = -kQ
```

with

```
k = 900 psia / 9000 tons = 0.1 psia / tons
```

Combining the two equations leads to the initial-value problem

```
dp/dt = -kα(p² - p*²)^β
p(0) = p₀
```

Solve this initial-value problem using a step size of Δt = 0.01 and performing 10 steps.

## 32. The following figure shows a circuit consisting of a coil wound around an iron core, a resistance, a switch, and a voltage source:

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_219_0.png)

The magnetization curve is given by the equation

```
Ni = 1/2 Φ + 3/1000 Φ³
```

where N = number of turns of coil, i = current (amperes), and Φ = flux in core (kilolines). Kirchoff’s law gives the differential equation

E = R i + L \frac{di}{dt} = R i + 10^{-5} \frac{d\Phi}{dt}

where L = self-inductance (henrys), R = resistance (ohms), and t = time (sec). Assume N = 100 and R = 500. Then

\frac{d\Phi}{dt} = E - 2.5\Phi' - 0.015\Phi^3, \quad \Phi(0) = 0

where t is now measured in milliseconds. For E = 20 V, solve this initial-value problem in the interval [0, 2] using a step size Δt = 0.01.

## 33. The number of individuals in a population is measured each year. Let P(t) denote the population at year t. Let α denote the birthrate, and assume that the death rate β is proportional to the size of the population, that is, β = γ P(t), where γ is a constant. Hence, the growth rate of the population is given by the logistic equation P'(t) = α P(t) − γ [P(t)]². Assume that P(0) = 50,000, α = 3 × 10⁻², and γ = 1.5 × 10⁻⁷. Solve this initial-value problem with step size Δt = 0.01 to find the population after 5 years.

## 34.–38. The Runge-Kutta method is a popular and one of the most accurate numerical methods for solving a first-order differential equation y' = f(x, y) with initial condition y(x₀) = y₀:

- 1. Select an x-increment Δx.
- 2. The approximate solution yₙ₊₁ at xₙ₊₁ = x₀ + (n + 1)Δx for n = 0, 1, 2, … is given by

yₙ₊₁ = yₙ + \frac{1}{6}(K₁ + 2K₂ + 2K₃ + K₄)

where

K₁ = Δx · f(xₙ, yₙ)

K₂ = Δx · f(xₙ + \frac{Δx}{2}, yₙ + \frac{K₁}{2})

K₃ = Δx · f(xₙ + \frac{Δx}{2}, yₙ + \frac{K₂}{2})

K₄ = Δx · f(xₙ + Δx, yₙ + K₃)

Write a program to implement the Runge-Kutta method and use it to solve Problems 29–33.

## Using Classes

## CONTENTS

- 7.1 Introductory Example: Internet Addresses 208
- 7.2 Introduction to Classes 211
- 7.3 The istream and ostream Classes 218
- 7.4 The string Class 228
- 7.5 The C++ complex Type 233
- 7.6 Simulation with Random Numbers: Shielding a Nuclear Reactor 240
- Chapter Summary 245
- Test Yourself 248
- Exercises 251
- Programming Problems 256

> There are three social classes in America: upper middle class, middle class, and lower middle class.
> 
> JUDITH MARTIN ("MISS MANNERS")

> A program is a spell cast over a computer, turning input into error messages.
> 
> ANONYMOUS

> For every complex problem there is an answer that is clear, simple, and wrong.
> 
> H. L. MENCKEN

> Carry out a random act of kindness, with no expectation of reward, safe in the knowledge that one day someone might do the same for you.
> 
> DIANA, PRINCESS OF WALES

THE WORD class IS often used to describe a group or category of objects that have a set of attributes in common. For example, the high school sports teams in one state are described as class A, class AA, class AAA, or class AAAA, depending on the number of students in the school. The usual classifications of secondary and college students are freshman, sophomore, junior, and senior. Metals, ceramics, polymers, semiconductors, and composites are classes of engineering materials, based on their chemical composition. The U.S. Navy uses Skipjack class, Thresher class, and Sturgeon class to characterize different kinds of submarines. Economists describe families as lower class, middle class, or upper class, based on their annual income. In these examples, class is used as a synonym for type because it provides a name for a group of related objects.

In Chapter 3, we studied the fundamental types provided in C++ to model basic objects such as numbers and characters: int, unsigned, double, char, bool, and variations of these such as short, long, and float. These types, however, cannot model more complex objects such as names of chemical elements, units of measurement, names and addresses of persons, and so on. None of the fundamental types, char type in particular, can adequately model these names because they consist of several characters and char values can only be single characters.

For situations like this, C++ provides libraries of standard classes to represent more complex objects. Also, programmers can build their own classes, thereby extending the C++ language. In this chapter, we will examine four standard C++ classes:

- the istream class to model input from a keyboard;
- the ostream class for modeling output to a screen;
- the string class for modeling sequences of characters;
- the complex class template to model complex numbers.

In the last section we will use

- a programmer-defined RandomInt class to generate random integers in a simulation program.

In Chapter 14 we will see how we can create our own classes.

### 7.1 INTRODUCTORY EXAMPLE: INTERNET ADDRESSES

IP (Internet Protocol) addresses are used to uniquely identify computers in the Internet; for example, titan.ksc.nasa.gov is the symbolic IP address of a site at the NASA Kennedy Space Center. Such an address is made up of four fields that represent specific parts of the Internet,

```
host.subdomain.subdomain.rootdomain
```

and is translated into a unique numeric IP address. This address is a 32-bit value, but it is usually represented in a dotted-decimal notation by separating the 32 bits into four 8-bit

fields, expressing each field as a decimal integer, and separating the fields with a period; for example, at the time of this writing, 163.205.10.1 was the IP address for the above site at the NASA Kennedy Space Center. Each of the four parts is an 8-bit integer, so the entire address can be stored in 32 bits.

### 7.1.1 Problem

A gateway is a device used to interconnect two different computer networks. Suppose that a gateway connects an engineering firm to the Internet and that the company’s network administrator needs to monitor connections through this gateway. Each time a connection is made, the IP address of the employee’s computer is transmitted to the network administrator, who analyzes the components that make up the address and records them.

### 7.1.2 Object-Centered Design

#### 7.1.2.1 Behavior

The program will display on the screen a prompt for an IP address. The user will enter a string of characters from the keyboard, which the program will read. The program will then compute and output its four network/host information blocks on the screen along with descriptive text, or display an error message if the user did not enter a valid address.

#### 7.1.2.2 Objects

From the statement of the desired behavior, we can identify the following objects:

| Problem Objects | Type | Kind | Name | |
|---|---|---|---|---|
| Software Objects | | | | |
| screen | output device | variable | cout | |
| prompt | text string | constant | none | |
| IP address | text string | variable | address | |
| keyboard | input device | variable | cin | |
| network/host information blocks | text string | variable | block1, block2, block3, block4 | |
| descriptive text error message | text string | constant | none | |

#### 7.1.2.3 Operations

Again, from the statement of the desired behavior, we can identify the following operations:

- i. Display a string on the screen.
- ii. Read a string from the keyboard.
- iii. Find each network/host information block and extract it from the string.
- iv. Display each information block on the screen.

#### 7.1.2.4 Algorithm

We now organize these operations into the following algorithm, which also shows how operation (iii) requires some refinement into simpler operations that are provided in C++.
