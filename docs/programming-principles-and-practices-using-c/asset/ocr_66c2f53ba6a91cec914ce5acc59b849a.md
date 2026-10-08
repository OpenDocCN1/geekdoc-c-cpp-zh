+   19.1 The problems

19.2 Changing size

- 19.2.1 Representation
- 19.2.2 reserve and capacity
- 19.2.3 resize
- 19.2.4 push_back
- 19.2.5 Assignment
- 19.2.6 Our vector so far

19.3 Templates

- 19.3.1 Types as template parameters
- 19.3.2 Generic programming
- 19.3.3 Concepts
- 19.3.4 Containers and inheritance
- 19.3.5 Integers as template parameters
- 19.3.6 Template argument deduction
- 19.3.7 Generalizing vector

+   19.4 Range checking and exceptions

- 19.4.1 An aside: design considerations
- 19.4.2 A confession: macros

19.5 Resources and exceptions

- 19.5.1 Potential resource management problems
- 19.5.2 Resource acquisition is initialization
- 19.5.3 Guarantees
- 19.5.4 unique_ptr
- 19.5.5 Return by moving
- 19.5.6 RAI1 for vector

# 19.1 The problems

At the end of Chapter 18, our **vector** reached the point where we can

+   - Create **vectors** of double-precision floating-point elements (objects of class **vector**) with whatever number of elements we want
- Copy our **vector** using assignment and initialization
- Rely on **vectors** to correctly release their memory when they go out of scope
- Access **vector** elements using the conventional subscript notation (on both the right-hand side and the left-hand side of an assignment)

That’s all good and useful, but to reach the level of sophistication we expect (based on experience with the standard library **vector**), we need to address three more concerns:

+   - How do we change the size of a **vector** (change the number of elements)?
- How do we catch and report out-of-range **vector** element access?
- How do we specify the element type of a **vector** as an argument?

For example, how do we define **vector** so that this is legal:

```
vector<double> vd; // elements of type double
for (double d; cin>>d; )
    vd.push_back(d); // grow vd to hold all the elements
```