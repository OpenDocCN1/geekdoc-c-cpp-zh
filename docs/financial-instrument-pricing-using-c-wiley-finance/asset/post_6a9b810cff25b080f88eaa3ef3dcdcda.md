
between pieces of functionality within a given module. For classes, *cohesion metrics* measure how well the member functions of a class are related to each other. In general, a cohesive class performs one function. A non-cohesive class performs two or more unrelated functions. Cohesion is a *qualitative measure* (we can speak of *high cohesion* and *low cohesion*, for example) and we can identify different forms of cohesion (McConnell, 2004, pp. 168–171), from worst to best. McConnell describes seven types but we restrict our attention to the three best ones. In the following the term module can refer to a class:

- *Communication/informational cohesion*: this occurs when parts of a module are grouped because they operate on the same data.
- *Sequential cohesion*: this occurs when parts of a module are grouped because the output from one part is the input to another part as in an assembly line.
- *Functional cohesion*: this occurs when parts of a module are grouped because they contribute to a single well-defined task of the module. This measure has a high correlation with SRP.

Functional cohesion is most desirable but it may not always be achievable. In general, modules with high cohesion have higher reliability and have fewer faults than low-cohesion modules.

We now give some low-level (but important) metrics related to class internals from Lorenz and Kidd (1994):

- M5: How many global and static variables used in a class.
- M6: Average number of arguments per member function.
- M7: Number of friend functions per class.
- M8: Average number of comment lines per member function.
- M9: Average number of commented methods.

However, many applications have the value zero for the metrics M8 and M9?

## 7.6.3 Class Coupling

This metric examines how classes relate to other classes, to subsystems and to other code. In particular, we are interested in the *dependencies* between classes. The more dependencies there are, the more difficult it is to understand and maintain the code.

Classes fulfil their responsibilities by collaborating with other classes. A *collaboration* represents a request from a client to a server in fulfilment of a *client responsibility* (Wirfs-Brock, Wilkerson and Wiener, 1990). For example, in a Monte Carlo simulation a client class that models a finite difference scheme collaborates with a server class that delivers random numbers. Identifying *collaborations* in the early stages of class design is important for a number of reasons:

- Information and control flow in an application is revealed.
- We are able to design an application as a graph of collaborating classes. This helps in distributing responsibilities among the collaborators.
- We can discover missing responsibilities by identifying a collaboration.
- We can identify a collaboration without an associated responsibility.

In order to identify collaborations we ask the following questions for each responsibility of each class:

- Is the class capable of fulfilling a given responsibility by itself?
- If not, what does the class need?
- From which other classes can the class acquire what it needs?

Knowing what the inter-class relationships are will be useful in identifying collaborations. The major relationships are:

- **R1: Composition** (‘is part of’). These are also called *Whole–Part* and aggregation relationships (see POSA, 1996).
- **R2: Has knowledge of.** This relationship is a more loosely coupled version of composition. In general, class *X* has knowledge of class *Y* if *Y* can provide information to *X*.
- **R3: Depends on.** This is similar to relationship R2 but the classes forming the relationship do not necessarily have to know about each other. A third-party mediator may know about the dependency, for example.

Having described what coupling is we now define the corresponding metrics:

- **M10:** The number of other classes that a given class collaborates with.
- **M11:** The amount of collaboration with other classes.

The metrics M10 and M11 will take on another form when we discuss software development based on system decomposition and interface specifications in Chapter 9. At that stage object-oriented technology fades into the background somewhat.

## 7.6.4 Class and Member Function Inheritance

This group of metrics revolves around the quality when we use inheritance:

- **M12:** Class hierarchy nesting level. This refers to the depth of the inheritance tree.
- **M13:** Number of abstract classes.
- **M14:** Use of multiple inheritance.
- **M15:** Number of member functions overridden by a derived class.
- **M16:** Number of member functions inherited by a derived class.
- **M17:** Number of member functions added by a derived class.

In general (as we discussed in Section 7.5), inheritance is a mixed blessing and we tend to avoid using it too much for the reasons alluded to in that section. We also have a number of alternative designs to reduce the numerical values corresponding to the metrics M12 to M17. It is clear that the higher the numerical value, the more difficult it is to maintain the class hierarchy and the less likely that it retains its *semantic integrity*. Some ways to reduce the value are:

1. Use static polymorphism with CRTP instead of subtype/dynamic polymorphism.
2. We could pretend that we live in an inheritance-free world and use composition throughout. But this approach is probably not realistic.
3. Create a single class C that contains one or more universal function wrappers. Then class C has constructors that accept functions as arguments. These functions replace `virtual` member functions and obviate the need for a class hierarchy to a certain extent.

We shall see more examples of these techniques as we progress in this book. In particular, they can be used to replace and upgrade the object-oriented design patterns in GOF (1995). Some of the concerns in Section 7.6 become non-issues in the new paradigm of system decomposition that we introduce in Chapter 9.

## 7.7 SUMMARY AND CONCLUSIONS

In this chapter we have discussed how to design classes using well-established modelling techniques and C++ language features. We design classes that are self-contained, robust and have loose coupling with other classes. This approach will hopefully be seen as an improvement on how classes are designed using class hierarchies and the approach will be generalised to the design of large systems in later chapters.

A special feature of this chapter is that we use the functional programming style (in particular `std::function`) to replace the virtual function by universal function wrappers. In particular, this allows us to reduce the potential explosion in the number of classes that need to be created in an application. One caveat is that we must pay attention to issues of efficiency.

## 7.8 EXERCISES AND PROJECTS

1. **(Explicit Constructors)**

   Consider the following class:

   ```cpp
   struct B
   {
       explicit B(int) {}
       explicit B(int, int) {}
       explicit operator int() const { return 0; }
   };
   ```

   Create a program to test the class. Which lines of code below compile and which ones do not? How would you modify the class to ensure that they do compile? Otherwise, how can these lines be modified so that the code compiles error free without modifying the class?

   ```cpp
   B b1 = 1;
   B b2(3);
   B b3{ 7, 3 };
   B b4 = (B)42;
   ```

2. Which of the following statements are advantages of using *deleted functions* compared to declaring these functions as `private` as in the C++98 standard?

   - **a)** Calling a deleted function will cause a compile-time error rather than a link error with C++98.
   - **b)** Use of a deleted function in an unevaluated expression leads to a link error.
   - **c)** Friends accessing a private function with missing definition experience a compile-time error.
   - **d)** Making deleted functions public results in better error messages in general.

3. In this exercise we investigate the copy constructor and copy assignment operator as default and deleted forms (there are four choices of default/delete for these two functions). One choice is:

   ```cpp
   // Copy ctor and copy assignment operator
   F(const F&) = delete;
   F& operator = (const F&) = delete;
   ```

   Test this and the three other options and determine which ones compile and which ones do not.

4. Which of the following statements are true?

   - a) constexpr applies to both objects and functions.
   - b) All const objects are also constexpr objects.
   - c) The output from a constexpr function will be known at compile-time if its input arguments are known at compile-time.
   - d) constexpr functions need not necessarily produce values that are known at compile-time.

5. Explain why the following member function of class Point does not compile:

   ```cpp
   constexpr double Distance(const Point& pt2) const
   {
       return std::sqrt((x - pt2.x)*(x - pt2.x) + (y - pt2.y)*(y - pt2.y));
   }
   ```

   Furthermore, does the following code compile?

   ```cpp
   constexpr Point p2(1.0, 2.0);
   double newVal = 3.0;
   p2.X(newVal);

   Point p3(1.0, 2.0);
   double newVal2 = 3.0;
   p3.X(newVal2);
   ```

6. Which two (most important) symptoms in your opinion can manifest themselves if a class does not satisfy SRP?

   - a) The number of methods in a class increases (threshold value ~ 12).
   - b) Class hierarchy nesting level (depth of inheritance hierarchy) (threshold value ~ 6).
   - c) Number of data members in a class (threshold value ~ 3).
   - d) Methods with many lines of code (threshold value ~ [10, 20]).

7. What is the Fragile Base Class Problem?

   - a) A base class which when modified can cause derived classes to malfunction.
   - b) A base class containing many abstract methods that must be overridden in derived classes.
