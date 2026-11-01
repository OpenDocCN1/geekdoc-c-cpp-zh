
To explain levels of abstraction, consider the seven-layer OSI model.² This model partitions a communication system into abstraction layers. Each layer exposes an interface to the next layer, but not to the previous layer. Engineers work in the layer that fits their specialty. For example, I am a software engineer rather than an electronics engineer. I would feel very uncomfortable working in layer 1, the physical layer, and much happier working in layer 7, the application layer. You may have heard the term “full-stack engineer.” This engineer is comfortable in all the layers. They are mythical creatures.

2. https://en.wikipedia.org/wiki/OSI_model

The levels of abstraction in the parsing problem can be described thus:

1. The streaming layer, which delivers a stream of data to...
2. The parsing layer, which delivers individual symbols to...
3. The dictionary layer, which matches symbols to tokens and delivers them to...
4. The token layer, which validates input and updates values

These abstractions are all distinct, nonoverlapping parts of the problem.

## Abstraction by refactoring and drawing the line

The key to abstraction is knowing where to draw the line that separates the different layers. As we remarked earlier, it is an art, not a science, but there are three things you can look for. First, excessive detail. Does the code spend time carrying out tasks that seem singularly unrelated to the task at hand? The Core Guideline for this chapter uses a busy for loop involving reading a file, validating, and performing reallocation as an example: there is too much going on in there. One can also consider designing baroque data structures especially for local use. Is this data structure of any use outside of this context? Will it ever be? If the answer is yes, take this data structure and move it from the code under examination to a more generic library. Separating detail into different libraries is a form of abstraction that is applicable to both the guideline example and the notion of pulling out data structures.

Second, verbose repetition. What sort of patterns can you see? Has there been some devious copying and pasting? Are you able to express them as an individual function or function template? Pull that code out into a function, give it a name, and rejoice in having identified an abstraction.

Third, and we would love a better word for this, wheel reinvention. This is slightly different from repetition and is a combination of the first two items. A lot of time has been spent identifying and naming the fundamental algorithms of computing. Make sure you are familiar with what they are and how they are offered through the standard library.

Repetition is a hint that there is an algorithm waiting to be uncovered, and a good algorithm is merely a concise description of what a piece of code does. In 2013 Sean Parent gave a talk called C++ Seasoning³, which spent much of the first half addressing the mantra “no raw loops.” His advice was to use an existing algorithm such as `std::find_if`, or implement a known algorithm as a function template and contribute it to an open source library, or devise a brand-new algorithm, write a paper about it, and become famous giving talks. This is excellent advice that will guide you on your way to eliminating messy code.

3. https://www.youtube.com/watch?v=W2tWOdzgXHA

## Summary

Messy code stops the reader from understanding at a glance what is going on. Avoid this by:

- Identifying patterns of existing code or existing algorithms, preferably as they happen, and lifting them out of the mess and abstracting them into their own function
- Identifying the different levels of abstraction
- Identifying how to encapsulate all these parts

## Chapter 2.2

### I.23: Keep the number of function arguments low

### How much should they earn?

Here’s a function declaration:

```cpp
double salary(PayGrade grade, int location_id);
```

It’s nice to see “double salary” at the start of a line of code; sadly, the purpose of this function is not to double your salary, but to report a salary for a particular pay grade at a particular location. Also, as remarked earlier, you should use integral types for money, so we shall redeclare this function, thus:

```cpp
int salary(PayGrade grade, int location_id);
```

You might see this sort of thing in a government contract: civil servant salaries are often pegged to a pay grade but will vary by location. In the UK, for example, some civil servants in London are paid more because of the increased cost of living in the capital.

This is a perfectly normal, ordinary function. It doesn’t appear to rely on external information and in all likelihood simply queries a database table to retrieve the data. It has the look and feel of a first attempt at a function: simple, unambiguous, quiet, unassuming.

Then one day, by act of parliament or some other great immovable object of irresistible progress, the requirements change, and salaries are now calculated based not only on pay grade and location, but also on length of service. Perhaps as an aid to retention, it has been decided that a small multiplying factor should be included for long-serving members of staff.

This is not a problem: we can simply add a parameter to the function to represent length of service. This is measured in years, so an `int` will do.

We now have

```cpp
int salary(PayGrade grade, int location_id, int years_of_service);
```

You might be looking at the pair of ints and answering the question “what could possibly go wrong” with “parameter inversion.” You make a mental note to see how many different locations there are, with a view to creating an enumeration so that the second parameter can be converted into a more narrowly focused type.

Time passes and, with a crashing inevitability, pay mechanisms change again, and another consideration emerges. This one is based on team size. There has been grumbling that management pay grades don’t reflect the additional burden of managing a team of more than 10 people. Rather than add a new pay grade, which would represent an enormous amount of bureaucratic negotiation, a new rule has been added for employees in the management pay grades that, as with long service, adds a small multiplying factor. This is a simple matter of passing in the number of reports, so we add a fourth parameter.

```cpp
int salary(PayGrade grade, int location_id, int years_of_service,
           int reports_count, bool* large_team_modifier);
```

The `reports_count` boundary depends on the pay grade. Above a certain pay grade, the multiplier comes into effect for managers of larger teams. However, the information about whether the multiplier is applied is important to other functions. After extensive discussion on a lengthy email thread about the merits of returning `std::pair<int,bool>` versus the function calculated a salary according to an employee’s details. On reflection, once that third parameter made an appearance in the function signature, the smart thing to do would have been to encapsulate the parameters into a single abstraction and call it `SalaryDetails`.

> Once you have a collection of state serving a purpose, possibly with some relationships between them, there is a chance that you have discovered an abstraction. Collect that state together into a single class, give it a name, and form those relationships into class invariants.

This is what is meant by missing an abstraction. Once you have a collection of state serving a purpose, possibly with some relationships between them, there is a chance that you have discovered an abstraction. Collect that state together into a single class, give it a name, and form those relationships into class invariants.

Applying this process to the salary function, we now have a struct called `SalaryDetails` that looks like this:

```cpp
struct SalaryDetails
{
    SalaryDetails(PayGrade grade_, int location_id_,
                  int years_of_service_,
                  int reports_count_);

    PayGrade pay_grade;
    int location_id;
    int years_of_service;
    int reports_count;
};
```

and a function signature that looks like this:
