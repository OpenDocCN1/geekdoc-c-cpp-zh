+   3. Why don\u0027t we just always define a **vector** with a large enough size for all eventualities?
4. How much spare space do we allocate for a new **vector**?
5. When must we copy **vector** elements to a new location?
6. Which **vector** operations can change the size of a **vector** after construction?
7. What is the value of a **vector** after a copy?
8. Which two operations define copy for **vector**?
9. What is the default meaning of copy for class objects?
10. What is a template?
11. What are the two most useful types of template arguments?
12. What is generic programming?
13. How does generic programming differ from object-oriented programming?
14. How does **array** differ from **vector**?
15. How does **array** differ from the built-in array?
16. How does **resize**() differ from **reserve**()?
17. What is a resource? Define and give examples.
18. What is a resource leak?
19. What is RAII? What problem does it address?
20. What is **unique_ptr** good for?

# Terms

+   * #define
* at()
* basic guarantee
* exception
* guarantee
* handle
* instantiation
* macro

+   * owner
* push_back()
* RAII
* resize()
* resource
* re-throw
* self-assignment
* shared_ptr

+   * specialization
* strong guarantee
* template
* template parameter
* this
* throw;
* unique_ptr

# Exercises

For each exercise, create and test (with output) a couple of objects of the defined classes to demonstrate that your design and implementation actually do what you think they do. Where exceptions are involved, this can require careful thought about where errors can occur.

+   1. Write a template function **f**( ) that adds the elements of one **vector\u003cT\u003e** to the elements of another; for example, **f**(v1,v2) should do **v1[i]+=v2[i]** for each element of **v1**.
2. Write a template function that takes a **vector\u003cT\u003e vt** and a **vector\u003cU\u003e vu** as arguments and returns the sum of all **vt[i]*vu[i]**s.