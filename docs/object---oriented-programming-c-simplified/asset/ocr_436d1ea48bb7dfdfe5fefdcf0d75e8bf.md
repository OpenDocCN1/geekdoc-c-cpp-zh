# 1. Bottom-Up and Top-Down Approaches

Any problem can be dealt with no ways viz top-down or bottom-up. A simple example is given here to illustrate the concept. Sorting an array of numbers involves the following :

+   (a) Comparison
+   (b) Exchange.

At the top level, an algorithm has to be formulated to carry out sorting using the above operations. Once the algorithm is confirmed, then the algorithms for comparison and exchange are formulated, before implementation of the entire algorithm. Therefore in this approach one begins from the top level without bothering about the minute details for implementation to start with.

The bottom-up approach is just the reverse. The lower level tasks are first carried out and are then integrated to provide the solution. In this method lower level structures are carried out. Here the algorithms for exchange and comparison will be formulated before formulating the algorithms for the whole problem.

In any case, dividing the problem into small tasks and then solving each task provides the solution. Therefore, either the top-down or bottom-up methodology has to be adopted for dividing the problem into smaller modules and then solving it. In the top-down methodology, the overall structure is defined before getting into details, but in the bottom-up approach, the details are worked out first before defining the overall structure.

# Points about Bottom-Up Approach

+   1. In bottom-up design individual parts of the system are specified in detail. The parts are then linked together to form larger components, which are in turn linked until a complete system is formed.
+   2. Bottom-up design yield programs which are smaller and more agile. A shorter program doesn't have to be divided into many components, and fewer components means program which are easier to read or modify.
+   3. Bottom-up design promotes code reusability. When you write two or more programs, many of the utilities you wrote for the first program will also be useful in the succeeding ones. That's why reusability of code is one of the main benefits of the bottom-up approach.
+   4. Bottom-up design makes programs easier to read.
+   5. Working bottom-up helps to clarify your ideas about the design of your program.
+   6. Bottom-up programming may allow you for unit testing, but until most of the system comes together none of the system can tested as a whole, often causing compilations near the end of the project.
+   7. An example of programming which uses this approaches is C++ and java.

# Points about Top-Down Approach

+   1. In the top-down model an overview of the system is formulated, without going into detail for any part of it. Each part of the system is then refined by designing it more detail.
+   2. Each new part may then be refined again, defining it in yet more detail until the entire specification is detailed enough to validate the model.