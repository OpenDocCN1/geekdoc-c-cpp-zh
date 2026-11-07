![](bbox=[0.363, 0.089, 0.8, 0.237])

**Figure 7.2**  Comparison of terms in real life and in object-oriented programming

> **Attributes of an object in object-oriented programming**  
> **are simulated using data members.**

# Member Function

In programming, a function is an entity that can do something. A **member function** in object-oriented programming is a function that simulates one of the behaviors of an object. For example, we can write a function that allows a circle to give its radius, its area, and its perimeter. We can also write a function that a circle can use to set its radius, but we should be aware of dependent attributes when we do so.

> **Behaviors of an object in object-oriented programming**  
> **are simulated using member functions.**

# 7.1.3 Comparison

Figure 7.2 shows the terms we use in real life and in object-oriented programming. The figure can be used throughout the chapter to better understand the concepts we discuss.

# 7.2 CLASSES

Although C++ has many predefined (built-in) types such as *int, double, char,* and *bool*, it also allows programmers to create new types. In C++, new types are mostly created using a **class**. To write object-oriented programs, we need to create a class, as a type, and then instantiate objects as instances of that type. In procedural programming, we need only write an *application* program (the *main* function and some other functions) to use objects of built-in types. In object-oriented programming we need three sections: the *class definition*, the *member function definition*, and the *application* (which uses the objects created from the class). In other words, if we want to write object-oriented programs versus writing procedural programs, we should always think about these three sections. We will see that sometimes each section is designed and saved by different entities. We have seen that in some cases, the first two sections (class definition and member function definitions) are created and stored in the C++ library (like the string and file classes), but the principle is the same: We need all three sections, as shown in Figure 7.3.

In the *class definition* section, we declare the data members and member functions. In the *member function definition* section, we define all member functions. In the *application* section, we instantiate objects and apply the member function to those objects.