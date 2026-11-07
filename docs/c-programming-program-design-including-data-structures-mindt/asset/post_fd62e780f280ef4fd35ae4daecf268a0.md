
## EXERCISES

The number in parentheses at the end of an exercise refers to the learning objective listed at the beginning of the chapter.

- 1. Mark the following statements as true or false.
  - a. The calculating device called the Pascaline could calculate sums up to eight figures long. (1)
  - b. All programs must be loaded into the CPU before they can be executed and all data must be loaded into main memory before it can be manipulated. (2)
  - c. Main memory is an ordered sequence of cells and each cell has a unique location in main memory. (2)
  - d. The program that loads first when you turn on your computer is called the operating system. (2)
  - e. Analog signals represent information with a sequence of 0s and 1s. (3)
  - f. The machine language is a sequence of 0s and 1s. (3)
  - g. A binary code is a sequence of 0s and 1s. (3)
  - h. A sequence of eight bits is called a byte. (3)
  - i. One GB is 2¹⁰ MB. (3)
  - j. In ASCII, A is the 65th character. (3)
  - k. The number system used by a computer is base 2. (3)
  - l. An assembler translates the assembly language instructions into machine language. (4)
  - m. A compiler translates the source program into an object program.
  - n. In a C++ program, statements that begin with the symbol # are called preprocessor directives. (7)
  - o. An object program is the machine language version of a high-level language program. (9)
  - p. All logical errors, such as division by 0, are reported by the compiler. (9)
  - q. In object-oriented design (OOD), a program is a collection of interacting objects. (10)
  - r. An object consists of data and operations on that data. (10)
  - s. ISO stands for International Organization for Standardization. (11)

- 2. Which hardware component performs arithmetic and logical operations? (2)
- 3. Which number system is used by a computer? (3)
- 4. What is an object program? (5)
- 5. What is linking? (8)
- 6. Which program loads the executable code from the main memory into the CPU for execution? (8)
- 7. In a C++ program, preprocessor directives begin with which symbol? (8)
- 8. In a C++ program, which program processes statements that begin with the symbol #? (8)
- 9. What is programming? (9)
- 10. What is an algorithm? (9)
- 11. Describe the steps required by the problem-solving process. (9)
- 12. Describe the steps required in the analysis phase of programming. (9)
- 13. Design an algorithm to find the weighted average of four test scores. The four test scores and their respective weights are given in the following format:

  ```text
  testScore weightTestScore
  ...
  ```

  (9)

- 14. Design an algorithm to convert the change given in quarters, dimes, nickels, and pennies into pennies. (9)
- 15. Given the radius, in inches, and price of a pizza, design an algorithm to find the price of the pizza per square inch. (9)
- 16. The dealer’s cost of a car is 85% of the listed price. The dealer would accept any offer that is at least $500 over the dealer’s cost. Design an algorithm that prompts the user to input the list price of the car and print the least amount that the dealer would accept for the car. (9)
- 17. The volume of a sphere is $(4.0 / 3.0)\pi r^3$ and the surface area is $4.0\pi r^2$, where $r$ is the radius of the sphere. Given the radius, design an algorithm that computes the volume and surface area of the sphere. Also using the C++ statements provided for Example 1-1, write the C++ statement corresponding to each statement in the algorithm. (You may assume that $\pi = 3.141592$.) (9)
- 18. Tom and Jerry opened a new lawn service. They provide three types of services: mowing, fertilizing, and planting trees. The cost of mowing is $35.00 per 5,000 square yards, fertilizing is $30.00 per application, and planting a tree is $50.00. Write an algorithm that prompts the user to enter the area of the lawn, the number of fertilizing applications, and the number of trees to be planted. The algorithm then determines the billing amount. (Assume that the user orders all three services.) (9)
- 19. Jason typically uses the Internet to buy various items. If the total cost of the items ordered, at one time, is $200 or more, then the shipping and handling is free; otherwise, the shipping and handling is $10 per item. Design an algorithm that prompts Jason to enter the number of items ordered and the price of each item. The algorithm then outputs the total billing amount. Your algorithm must use a loop (repetition structure) to get the price of each item. (For simplicity, you may assume that Jason orders no more than five items at a time.) (9)
- 20. An ATM allows a customer to withdraw a maximum of $500 per day. If a customer withdraws more than $300, the service charge is 4% of the amount over $300. If the customer does not have sufficient money in the account, the ATM informs the customer about the insufficient funds and gives the customer the option to withdraw the money for a service charge of $25.00. If there is no money in the account or if the account balance is negative, the ATM does not allow the customer to withdraw any money. If the amount to be withdrawn is greater than $500, the ATM informs the customer about the maximum amount that can be withdrawn. Write an algorithm that allows the customer to enter the amount to be withdrawn. The algorithm then checks the total amount in the account, dispenses the money to the customer, and debits the account by the amount withdrawn and the service charges, if any. (9)
- 21. Design an algorithm to find the real roots of a quadratic equation of the form $ax^2 + bx + c = 0$, where $a$, $b$, and $c$ are real numbers, and $a$ is nonzero. (9)
- 22. A student spends a majority of his weekend playing and watching sports, thereby tiring him out and leading him to oversleep and often miss his Monday 8 AM math class. Suppose that the tuition per semester is $25,000 and the average semester consists of 15 units. If the math class meets three days a week, one hour each day for 15 weeks, and is a four-unit course, how much does each hour of math class cost the student? Design an algorithm that computes the cost of each math class. (9)
- 23. You are given a list of students’ names and their test scores. Design an algorithm that does the following:
  - a. Calculates the average test scores.
  - b. Determines and prints the names of all the students whose test scores are below the average test score.
  - c. Determines the highest test score.
  - d. Prints the names of all the students whose test scores are the same as the highest test score.

  (Each of the parts a, b, c, and d must be solved as a subproblem. The main algorithm combines the solutions of the subproblems.) (9)

In this chapter, you will learn the basics of C++. As your objective is to learn the C++ programming language, two questions naturally arise. First, what is a computer program? Second, what is programming? A **computer program**, or a program, is a sequence of statements whose objective is to accomplish a task. **Programming** is a process of planning and creating a program. These two definitions tell the truth, but not the whole truth, about programming. It may very well take an entire book to give a good and satisfactory definition of programming. You might gain a better grasp of the nature of programming from an analogy, so let us turn to a topic about which almost everyone has some knowledge—cooking. A recipe is also a program, and everyone with some cooking experience can agree on the following:

- 1. It is usually easier to follow a recipe than to create one.
- 2. There are good recipes and there are bad recipes.
- 3. Some recipes are easy to follow and some are not easy to follow.
- 4. Some recipes produce reliable results and some do not.
- 5. You must have some knowledge of how to use cooking tools to follow a recipe to completion.
- 6. To create good new recipes, you must have a lot of knowledge and a good understanding of cooking.

These same six points are also true about programming. Let us take the cooking analogy one step further. Suppose you need to teach someone how to become a chef. How would you go about it? Would you first introduce the person to good food, hoping that a taste for good food develops? Would you have the person follow recipe after recipe in the hope that some of it rubs off? Or would you first teach the use of tools and the nature of ingredients, the foods and spices, and explain how they fit together? Just as there is disagreement about how to teach cooking, there is disagreement about how to teach programming.

Learning a programming language is like learning to become a chef or learning to play a musical instrument. All three require direct interaction with the tools. You cannot become a good chef just by reading recipes. Similarly, you cannot become a musician by reading books about musical instruments. The same is true of programming. You must have a fundamental knowledge of the language, and you must test your programs on the computer to make sure that each program does what it is supposed to do.

## A Quick Look at a C++ Program

In this chapter, you will learn the basic elements and concepts of the C++ programming language to create C++ programs. In addition to giving examples to illustrate various concepts, we will also show C++ programs to clarify these concepts. In this section, we provide an example of a C++ program that computes the perimeter and area of a rectangle. At this point you need not be too concerned with the details of this program. You only need to know the effect of an *output* statement, which is introduced in this chapter.
