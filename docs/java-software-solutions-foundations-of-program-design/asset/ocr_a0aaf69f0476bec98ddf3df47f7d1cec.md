```
SR 6.16 final int NUMROLLS = 100;
    int sum = 0;
    for (int i = 1; i <= NUMROLLS; i++)
    {
        sum += die.roll();
    }
    System.out.println((double)sum/NUMROLLS);
```

# Chapter 7 Object-Oriented Design

# 7.1 Software Development Activities

SR 7.1 The four basic activities in software development are requirements analysis (deciding what the program should do), design (deciding how to do it), implementation (writing the solution in source code), and testing (validating the implementation).

SR 7.2 Typically the client provides an initial set of requirements or a description of a problem they would like to have solved. It is the responsibility of the software developer to work with the client to make sure the requirements or problem statement is correct and unambiguous.

SR 7.3 Software development is a problem-solving activity. Therefore, it is not surprising that the four basic development activities presented in this section are essentially the same as the five general problem-solving steps presented in Section 1.6. “Establishing the requirements” directly corresponds to “understanding the problem.” “Designing a solution” and “considering alternative designs” taken together correspond to “creating a design”—in the case of software, the design is the solution. Finally, in both approaches we include “implementation” and “testing” stages.

# 7.2 Identifying Classes and Objects

SR 7.4 Identifying the nouns in a problem specification can help you identify potential classes to use when developing an object-oriented solution to a problem. The nouns in the specification often correspond to objects that should be represented in the solution.

SR 7.5 It is not crucial to identify and define all the methods that a class will contain during the early stages of problem solution design. It is often sufficient to just identify those methods that provide the primary responsibilities of the class. Additional methods can be added to a class as needed, when you evolve and add detail to your design.