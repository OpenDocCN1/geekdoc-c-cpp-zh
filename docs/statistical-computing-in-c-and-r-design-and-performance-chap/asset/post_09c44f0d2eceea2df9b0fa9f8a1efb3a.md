
# 326 NUMERICAL OPTIMIZATION

running times (measured via the clock function discussed in Section 3.8) and in terms of the total number of iterations.

- 8.25. Repeat Exercise 8.24 except with all functions written in R. For timing purposes you can use the system.time function discussed in Section 5.4.

- 8.26. Describe how golden section or bisection algorithms can be used to numerically evaluate the quantile function for a continuous distribution. Implement this approach as a quantile function in C++ and evaluate its performance in the case of the exponential distribution (where the quantile function is known and given in Section 4.6) and for the normal distribution. There is no closed form for the normal cumulative distribution function and it must be evaluated numerically. The function pnorm from the R Math Library or the R API performs this and can be used for your code.

- 8.27. Repeat the code development of Exercise 8.26 except with the optimize function in R.

- 8.28. The R function unroot can be used to find the zeros of a function. Write an R function that uses unroot to find a specified quantile of a cumulative distribution function. Assess the performance of your code with the exponential and normal distributions and compare it to the bisection and golden section algorithms of Exercises 8.26-8.27.

- 8.29. Develop a derivative of the C++ Like class in R. Construct a new method for mle that can be used on objects from your class. [Note: The stats4 package contains a likelihood class mle-class. So, this name should be avoided.

- 8.30. Create a set of code that will allow you to replicate the C++ and R maximum likelihood examples for the exponential distribution in Section 8.5.

- 8.31. A standard result concerning Fisher information is that (under regularity conditions) when $\theta^*$ is the true parameter value

$$E\left[\left(\frac{\partial f(X;\theta^*)}{\partial\theta}\right)^2\right]=-E\left[\frac{\partial^2 f(X;\theta^*)}{\partial\theta^2}\right]$$

This suggests an alternative strategy where the second derivative of the likelihood function is replaced with

$$\sum_{i=1}^n \left(\frac{\partial f(x_i;\theta)}{\partial\theta}\right)^2$$

This approach is called Fisher scoring and has the advantage of circumventing the need for evaluation of a second derivative. Modify the Like class to incorporate a method that uses Fisher scoring and compare its performance to the mle method.

# Chapter 9

# Abstract data structures

## 9.1 Introduction

The developments in Chapters 5-8 focused on methods for computing various quantities of statistical interest. Very little thought was given to the data that was used in the illustrative examples beyond being appropriate for with the method and in a form that was readily accessible to the program or function that used it in calculations. In practice, neither of these properties are likely to be manipulated (e.g., ordered, subsetted, etc.) to carry out the desired analysis of problem. Instead, the data will need to be manipulated to perform the desired analyses. Thus, the development of effective statistical methods must begin at the point of access to the data with the creation of algorithms to perform the requisite manipulations. The form of such algorithms is dictated by the way the data is stored. As a result, the design of data storage methods can be viewed as the statistical analog of experimental design; experiments must be run in a way that makes the factors of interest estimable, and similarly, data must be stored in a way that makes it possible to perform the proper analysis.

Now our primary vehicle for storing data has been an array. Although arrays work well for many applications, there are situations that arise where they become unwieldy to the point of being impractical. For example, they are not ideal for dealing with data sets that grow or shrink in a manner that requires frequent resizing of storage container. Similarly, insertion of new elements or deletion of current ones from an array will require shifting of the other elements which can be prohibitively consuming when such operations are commonplace. Fortunately, there are alternatives to array storage that provide great flexibility in tailoring a particular storage method to work with the data at hand.

In the next chapters we explore the concept of data storage from the perspective of abstract structures or abstract types (ADTs, subsequently). In a general sense, an ADT represents a model for storing and organizing data in a way that simplifies the computations that are of interest and, in some cases, makes the desired computations possible. They generally come equipped with operations that let us efficiently, modify (e.g., insert or delete) and carry out computations (e.g., sorting) with the stored data. What distinguishes one ADT from another is not only the space required to hold the data (often referred to as space complexity), but also the associated efficiency, in terms of execution time, of the operations it provides under its particular storage paradigm (often referred to as time complexity). Although our discussions will pay some attention to the space and computation issues beyond what can be presented here. Detailed studies of these areas are provided, for example, in Papadimittrou (1994) and Arakan and Barak (2009).

The collection of all ADTs represents a data storage toolbox of sorts. In respect that the proper tool should be selected for the storage job at hand. For example, if one has data that needs to be maintained in a particular order while easily allowing element insertion, the linked list structure of Section 9.2.2 serves as a good option. For this type of ADT insertion and deletion operations involve a fixed time expense that is independent of the number of elements in the data set. Searching for specific elements is another ter and this type of operation requires an effort that grows linearly with the data size. For situations where searches are an important part of the data management, the chaining hash table of Section 9.2.4 may provide a better option wherein searching and deletion tasks can be carried out in nearly constant time.

# ABSTRACT DATA STRUCTURES

The present chapter gives a high level overview of ADTs. Our perspective is here much the same as for a class declaration in C++. As a case in point, the listing below is the declaration for a pared down version of our Vector class.

```cpp
class Vector{
  double* pA;
  int nRows;

public:
  Vector(int nRows, double const* pa);
  Vector(const Vector& v);
  Vector();
  Vector& operator=(const Vector& v);
  double operator[](int i) const {return pA[i];}
};
```

This declaration can be viewed as a contract that guarantees i) Vector objects can be created, ii) a Vector may be assigned to another and iii) random access using operator[] will be to the elements of the underlying array that is encapsulated by a Vector object.

There is nothing special about using doubles for array elements, as in Exercise 3.31, a template approach can be used to allow them both of int or char, for example. Taking this one step further leads to Vector objects that serves as containers in the sense of being able to hold arbitrary, user-defined types. But, even in this generic form the operations laid out in the Vector declaration make sense and represent at least the minimum one would want from something that provides a generalization of a numeric array; i.e., a generic container class should include functions that

- a) create a new object,
- b) create a copy of an existing Vector object,
- c) assign a Vector object to another
- d) allow (random) access to the objects in the container.

This list of operations represents a public interface for a Vector class in the same sense as a class declaration.

Our treatment of ADTs in this chapter will be geared towards describing their public interfaces through abstract, somewhat axiomatic "statements" that indicate how the data will be stored and the operations will be expected from the structure. This will be supplemented by pseudo-code implementations of the operations. In this case, specific examples of simple C++ implementations will be provided to illustrate the concept with a (relative) minimum of technical clutter. The R language has certain AD capabilities that will be explored here.

Much of the code development in this chapter illustrates how to build ADT implementations from the ground up. The resulting structures are simplistic in nature and of conceptual,
