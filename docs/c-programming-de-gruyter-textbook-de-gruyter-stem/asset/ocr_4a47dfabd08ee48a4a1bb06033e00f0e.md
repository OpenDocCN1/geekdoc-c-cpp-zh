# # 10 Generic Programming and the Standard Template Library

In Chapter 9, we introduced several basic collections and related algorithms. There are many other types of commonly used collections and complex algorithms. The study of these issues is the subject of data structure. It is not necessary for programmers to develop every class and algorithm from scratch. In fact, the standardization and modularization of commonly used algorithms are the keys to fast software production. To achieve this, we need to use only concepts from object-oriented programs but also those from generic programming. The Standard Template Library (STL) in C++ is a good example of integrating these concepts.

In this chapter we introduce the concepts, the structures, and the usage of STL. We briefly introduce the basic applications of containers, iterators, algorithms, and function objects to get an overall picture of STL. We recommend readers refer to other books for other topics in STL and generic programming. Grasping some basic knowledge in data structure helps to understand the materials in this chapter.

# ## 10.1 Generic Programming

# ### 10.1.1 Introduction

The goal of generic programming is to represent abstract concepts and algorithms in generic codes without losing efficiency. Generic programming is a different technique from object-oriented programming. In some cases, there are even conflicts between generic programming design and good object-oriented programming design. But the combination of these two techniques results in a powerful tool for building complex software. STL is an excellent example of it. For example, with the help of STL, programmers do not need to write array classes for integers, reals, and characters; writing a generic template is sufficient. These techniques allow high code reuse and improve the efficiency of software production.

Recall the array, linked list, and the queue template implementation, and sorting algorithm discussed in Chapter 9. In object-oriented programming, it is good practice to encapsulate these algorithms into classes. However, a better solution is to write generic algorithms independent of implementation such "finding an element sequentially in a linear collection". That is the goal of generic programming.

The iterator is the adaptive layer between the algorithms and the data structure. Algorithms can use the iterator interface to access the data structure to perform specific operations. That is the key scheme for decoupling the data structure and the algorithm used by generic programming.