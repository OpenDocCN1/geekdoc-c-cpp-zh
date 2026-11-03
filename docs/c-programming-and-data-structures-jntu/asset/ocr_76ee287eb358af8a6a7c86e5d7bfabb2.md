# Chapter 14

# Data Structures

# 14.1 INTRODUCTION TO DATA STRUCTURES

In the field of computing, we have formulated many ways to handle data efficiently. So far, we have seen how to use variables to store data. However, variables are not feasible when handling a huge amount of data.

Consider a situation when we want to access information, such as student name, roll no, section name, sex, address, subjects, and marks obtained in each subject for students in a specific state of the country. With a single variable, it is an unfeasible task to store such a large amount of related data. Also, we need an organized medium of storage to handle any correlated information. Thus, the concept of data structure is introduced.

Data structure is a collection of organized data that are related to each other. Data structures can be classified into two types:

+   - Linear data structure
+   - Non-linear data structure

The linear data structures, such as array and list, and non-linear data structures, such as trees and graphs, are most popularly known data structures.

As we have seen earlier, an array is used to store data in consecutive memory locations. Arrays are considered as a good example for implementing simple data structures. Arrays can be effectively used for random access of fixed amount of data. We can also use arrays to create data structures, such as stack and queue. Stacks and queues are usually known as linear data structures, because data items in stacks and queues are arranged in a linear sequence.

# 14.2 STACKS

A stack is a linear data structure in which a data item is inserted and deleted at one end. A stack is called a Last In First Out (LIFO) structure because the data item that is inserted last into the stack is the first data item to be deleted from the stack. To understand this, imagine a pile of books. Usually, we pick up the topmost book from the pile. Similarly, the topmost item (i.e. the item which made the entry last) is the first one to be picked up/removed from the stack.