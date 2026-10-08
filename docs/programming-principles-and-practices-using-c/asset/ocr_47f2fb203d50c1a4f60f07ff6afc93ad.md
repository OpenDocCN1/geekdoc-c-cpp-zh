+   * **Predicate<P,T<>**: We can call **P** with an argument of type **T** to get a Boolean result.
* **Binary_predicate<P,T<>**: We can call **P** with two arguments of type **T** to get a Boolean result.
* **Binary_predicate<P,T,U<>**: We can call **P** with arguments of types **T** and **U** to get a Boolean result.
* **Less_comparable<L,T<>**: We can use **L** to compare two **Ts** for less than using **<** to get a Boolean result.
* **Less_comparable<L,T,U<>**: We can use **L** to compare a **T** to a **U** for less than using **<** to get a Boolean result.
* **Binary_operation<B,T,U<>**: We can use **B** to do an operation on two **Ts**.
* **Binary_operation<B,T,U<>**: We can use **B** to do an operation on a **T** and a **U**.
* **Number<N<>**: **N** behaves like a number, supporting **+**, **-**, and **/**.

For standard library containers and algorithms, these concepts (and many more) are specified in excruciating detail. Here, especially in Chapters 20 and 21, we will use them informally to document our containers and algorithms.

A container type and an iterator type, **T**, have a value type (written as **Value_type<T>>**), which is the element type. Often, that **Value_type<T>>** is a member type **T::value_type**; see **vector** and **list** (§20.5).

# 19.3.4 Containers and inheritance

There is one kind of combination of object-oriented programming and generic programming that people always try, but it doesn't work: attempting to use a container of objects of a derived class as a container of objects of a base class. For example:

```
vector<Shape> vs;
vector<Circle> vc;
vs = vc; // error: vector<Shape> required
void f(vector<Shape>&);
f(vc); // error: vector<Shape> required
```

But why not? After all, you say, I can convert a **Circle** to a **Shape**! Actually, no, you can't. You can convert a **Circle*** to a **Shape*** and a **Circle&** to a **Shape&**, but we deliberately disabled assignment of **Shapes**, so that you wouldn't have to wonder what would happen if you put a **Circle** with a radius into a **Shape** variable that doesn't have a radius (§14.2.4). What would have happened — had we allowed