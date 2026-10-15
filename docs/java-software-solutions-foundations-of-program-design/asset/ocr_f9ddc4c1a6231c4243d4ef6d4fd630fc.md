During software design, alternatives need to be considered and explored. Often, the first attempt at a design is not the best solution. Fortunately, changes are relatively easy to make during the design stage.

Implementation is the process of writing the source code that will solve the problem. More precisely, implementation is the act of translating the design into a particular programming language. Too many programmers focus on implementation exclusively when actually it should be the least creative of all development activities. The important decisions should be made when establishing the requirements and creating the design.

Testing is the act of ensuring that a program will solve the intended problem given all of the constraints under which it must perform. Testing includes running a program multiple times with various inputs and carefully scrutinizing the results. But it means far more than that. We revisit the issues related to testing in Section 7.9.

KEY CONCEPT
The effort put into design is both crucial and cost-effective.

# SELF-REVIEW QUESTIONS (see answers in Appendix N)

+   SR 7.1 Name the four basic activities that are involved in a software development process.
+   SR 7.2 Who creates/specifies software requirements, the client or the developer? Discuss.
+   SR 7.3 Compare and contrast the four basic development activities presented in this section with the five general problem-solving steps presented in Section 1.6.

# 7.2 Identifying Classes and Objects

A fundamental part of object-oriented software design is determining the classes that will contribute to the program. We have to carefully consider how we want to represent the various elements that make up the overall solution. These classes determine the objects that we will manage in the system.

One way to identify potential classes is to identify the objects discussed in the program requirements. Objects are generally nouns. You literally may want to scrutinize a problem description, or a functional specification if available, to identify the nouns found in it. For example, Figure 7.1 shows part of a problem description with the nouns circled.

Of course, not every noun in the problem specification will correspond to a class in your program. This activity is just a starting point that allows you to think about the types of objects a program will manage.

KEY CONCEPT
The nouns in a problem description may indicate some of the classes and objects needed in a program.