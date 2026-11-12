program to another as you track down an error. The time you spend on these functions often proves to be worthwhile, as you can call them repeatedly while debugging different parts of the program.

Hopefully, this discussion has conveyed the importance of the effective use of diagnostic aids in debugging. Even the best programmers have to spend some time debugging. Thus, to be a truly good programmer, you must be a good debugger.

# B.7 Testing

You can never test a program too much

Programs need to be tested to make sure that they correctly solve their current requirements. Good testing cannot happen without a plan. Software is complex, and determining whether it works correctly is not easy. Software testing is so important that some iterative development processes argue that tests should be developed before writing any code.

# B.7.1 Levels of Testing

Unit testing checks individual modules

Several levels of testing should take place. The first level of testing is called unit testing, and it happens on the individual modules. You should test individual methods first, and then test the classes. The second level of testing is called integration testing, and it tests the interactions among modules. The next level of testing is called system testing, in which the entire program is tested. Finally, a special type of testing called acceptance testing shows whether the system as a whole complies with its requirements.

Unit testing is something that you have probably done before. It is closely related to some of the ideas talked about in the previous debugging section. A function is tested to make sure that it conforms to its requirements. Often with small programs, testing does not go beyond this level.

Integration testing checks many parts of a solution together

One way to perform integration tests is to make sure that the various objects within a program correctly implement the interactions in your design. Integration testing can be challenging, because there are many ways in which the objects in a program can interact. It is difficult to make sure they do what they are designed to do and nothing more.

System testing checks the integration of the solution with other systems

System testing entails running the program in the environment in which it was designed to work. Here the program is tested to make sure that it interacts with external systems correctly. The external systems might be other programs—such as a government tax collection system—or hardware devices.

# B.7.2 Kinds of Testing

Two kinds of testing can be applied to a system:

+   • Open-box testing. With open-box, white-box, or glass-box testing, you design tests knowing how the modules work. You carefully choose a method's actual arguments in a way that exercises all lines of code in the method. For example, you must make sure that all branches of if and switch statements are executed.

+   • Closed-box testing. With closed-box, black-box, or functional testing, you know the name of the method being tested, as well as its argument list, its return type, and its operation contract. Using only this information, you develop tests across a range of valid input, and then check the output against hand-calculated results. Choosing some actual arguments outside of their valid range tests how the module handles incorrect input.

# B.7.3 Developing Test Data

The test data that you use must test a wide range of conditions. It should include valid, typical input and values at the extreme limits of valid data—called boundary values—as well as values that