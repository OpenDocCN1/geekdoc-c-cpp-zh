
20 Chap. 1 Data Structures and Algorithms

of arts. The novice designer can jump-start the learning process by studying known and well-used design patterns. The classic reference on design patterns is Design Patterns: Elements of Reusable Object-Oriented Software by Gamma, Helm, Johnson, and Vlissides [GHJV95] (this is commonly referred to as the “gang of four”). Unfortunately, this is an extremely difficult book to understand, in part because the concepts are inherently difficult. A number of Web sites are available that discuss design patterns, and which provide study guides for the Design Patterns. Two other books that discuss object-oriented software design are Object-Oriented Software Design and Construction with C++ by Dennis Kafura [Raf98], and Object-Oriented Design Heuristics by Arthur. Riel [Rie96].

## 1.6 Exercises

The exercises for this chapter are different from those in the rest of the book. Most of these exercises are answered in the following chapters. However, you should look up the answers in other parts of the book. These exercises are intended to make you think some about the issues to be covered later. Answer them to the best of your ability with your current knowledge.

- 1.1 Think of a program you have used that is unacceptable slow. Identify the specific operations that make the program flow. Identify other basic operations that the program performs quickly enough.

- 1.2 Most programming languages have a built-in data type. Normally this representation has a fixed size, placing a limit on how large a value can be stored in an integer variable. Describe a representation for integers that has no size restriction (other the limits of the computer’s available main memory), and thus no practical limit on how large an integer can be stored. Briefly show how your representation can be used to implement the operations of addition, multiplication, and exponentiation.

- 1.3 Define an ADT for character strings. Your ADT should consist of typical functions that can be performed on strings, with each function defined in terms of its input and output. Then define two different physical representations for strings.

- 1.4 Define an ADT for a list of integers. First, decide what functionality your ADT should provide. Example 1.4 should give you some ideas. Then, specify your ADT in C++ in the form of an abstract class definition, showing the functions, their parameters, and their return types.

- 1.5 Briefly describe how integer variables are typically represented on a computer. (Look up one’s complement and two’s complement arithmetic in an introductory computer science textbook if you are not familiar with these.)

Why does this representation for integers qualify as a data structure as defined in Section 1.2?

- 1.6 Define an ADT for a two-dimensional array of integers. Specify precisely the basic operations that can be performed on such arrays. Next, imagine an application that stores an array with 1000 rows and 1000 columns, where less than 10,000 of the array values are non-zero. Describe two different implementations for such arrays that would be more space efficient than a standard two-dimensional array implementation requiring one million positions.

- 1.7 Imagine that you have been assigned to implement a sorting program. The goal is to make this program general purpose, in that you don't want to define in advance what key types are used. Describe ways to generalize a simple sorting algorithm (such as insertion sort, or any other sort you are familiar with) to support this generalization.

- 1.8 Imagine that you have been assigned to implement a simple sequential search on an array. The problem is that you want the search to be as general as possible. This means that you need to support arbitrary record and key types. Describe ways to generalize the search function to support this goal. Consider the possibility that the function will be used multiple times in the same program, by differing record types. Consider the possibility that the function will need to be used on different keys (possibly with the same or different types) of the same record. For example, a student data record might be searched by zip code, by salary, or by a GPA.

- 1.9 Does every problem have an algorithm?

- 1.10 Does every algorithm have a C++ program?

- 1.11 Consider the design for a spelling checker program meant to run on a home computer. The spelling checker should be able to handle quickly a document of less than twenty pages. Assume that the spelling checker comes with a dictionary of about 20,000 words. What primitive operations must be implemented on the dictionary, and what is a reasonable time constraint for each operation?

- 1.12 Imagine that you have been hired to design a database system containing information about cities and towns in the United States, as described in Example 1.2. Suggest two possible implementations for the database.

- 1.13 Imagine that you are given an array of records that is sorted with respect to some key field contained in each record. Give two different algorithms for searching the array to find the record with a specified key value. Which one do you consider “better” and why?

- 1.14 How would you go about comparing two proposed algorithms for sorting an array of integers? In particular,

  - (a) What would be appropriate measures of cost to use as a basis for comparing the two sorting algorithms?
  - (b) What tests or analysis would you conduct to determine how the two algorithms perform under these cost measures?

- 1.15 A common problem for compilers and text editors is to determine if the parentheses (or other brackets) in a string are balanced and properly nested. For example, the string "((()))" contains properly nested pairs of parentheses, but the string "()()" does not, and the string "())" does not contain properly matching parentheses.

  - (a) Give an algorithm that returns true if a string contains properly nested and balanced parentheses, and false otherwise. Hint: At no time while scanning a legal string from left to right will you encounter more right than left parentheses
  - (b) Give an algorithm that returns the position in the string of the first parenthesis if the string is not properly nested and balanced. That is, if an excess right parenthesis is found, return its position; if there are too many left parentheses, return the position of the first left parenthesis. Return -1 if the string is properly balanced and nested.

- 1.16 A graph consists of a set of objects (called vertices) and a set of edges, where each edge connects two vertices. Any pair of vertices can be connected by only one edge. Describe at least two different ways to represent the connections defined by the vertices and edges of a graph.

- 1.17 Imagine that you are a shipping clerk for a large company. You have been handed 100 invoices, each of which is a single sheet of paper with a number in the upper right corner. The invoices must be sorted by this number, from lowest to highest. Write down as many different approaches to sorting the invoices as you can think of.

- 1.18 Would you want to sort an array of 1000 integers from lowest value to highest value? Write down at least five approaches to sorting the array. Do not write algorithms in C++ or pseudocode. Write a sentence or two for each approach to describe how it would work.

- 1.19 Think of an algorithm to find the maximum value in an (unsorted) array. Now, think of an algorithm to find the second largest value in the array. Which is harder to implement? Which takes more time to run (as measured by the number of comparisons performed)? Now, think of an algorithm to find the third largest value. Finally, think of an algorithm to find the middle value. Which is the most difficult of these problems to solve?

- 1.20 An unsorted list allows for constant-time insertion by adding a new element at the end of the list. Unfortunately, searching for the element with key X requires a sequential search through the unsorted list until X is found, which on average requires looking at half the list element. On the other hand, a
