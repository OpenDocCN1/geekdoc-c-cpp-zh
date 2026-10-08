
classes A and B into a "reusable component" called C. By providing the union of A's and B's interfaces, the introduction of C complicates our code:

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_846_0.png)

Here, both User 1 and User 2 use C. Unless you look into C, you might think that User 1 and User 2 gained benefits from sharing a popular component. Benefits from sharing ("reuse") would (in this case, wrongly) be assumed to include better testing, less total code, larger user base, etc. Unfortunately, except for a bit of oversimplification, this is not a particularly rare phenomenon.

What would help? Maybe a common interface to A and B could be provided:

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_846_1.png)

These diagrams are intended to suggest inheritance and parameterization, respectively. In both cases, the interface provided must be smaller than a simple union of A's and B's interfaces for the exercise to be worthwhile. In other words, A and B have to have a fundamental commonality for users to benefit from. Note how we again came back to interfaces (§9.7, §25.4.2) and by implication to invariants (§9.4.3).

### 22.1.2.6 Consistency and minimalism

Consistency and minimalism are primarily ideals for expressing ideas. So we might dismiss them as being about appearance. However, it is really hard to present a messy design elegantly, so demands of consistency and minimalism can be used as design criteria and affect even the most minute details of a program:

- Don't add a feature if you are in doubt about its utility.
- Do give similar facilities similar interfaces (and names), but only if the similarity is fundamental.
- Do give different facilities different names (and possibly different interface styles), but only if the differences are fundamental.

Consistent naming, interface style, and implementation style help maintenance. When code is consistent, a new programmer doesn’t have to learn a new set of conventions for every part of a large system. The STL is an example (Chapters 20–21, §B.4–6). When such consistency is impossible (for example, for ancient code or code in another language), it can be an idea to supply an interface that matches the style of the rest of the program. The alternative is to let the foreign (“strange,” “poor”) style infect every part of a program that needs to access the offending code.

One way of preserving minimalism and consistency is to carefully (and consistently) document every interface. That way, inconsistencies and duplication are more likely to be noticed. Documenting pre-conditions, post-conditions, and invariants can be especially useful as can careful attention to resource management and error reporting. A consistent error-handling and resource management strategy is essential for simplicity (§19.5).

To some programmers, the key design principle is KISS (“Keep It Simple, Stupid”). We have even heard it claimed that KISS is the only worthwhile design principle. However, we prefer less evocative formulations, such as “Keep simple things simple” and “Keep it simple: as simple as possible, but no simpler.” The latter is a quote from Albert Einstein, which reflects that there is a danger of simplifying beyond the point where it makes sense, thus damaging the design. The obvious question is, “Simple for whom and compared to what?”

### 22.1.3 Styles/paradigms

When we design and implement a program, we aim for a consistent style. C++ supports four major styles that can be considered fundamental:

- Procedural programming
- Data abstraction
- Object-oriented programming
- Generic programming

These are sometimes (somewhat pompously) called “programming paradigms.” There are many more “paradigms,” such as functional programming, logic programming, rule-based programming, constraints-based programming, and aspect-oriented programming. However, C++ doesn’t support those directly, and we just can’t cover everything in a single beginner’s book, so we’ll leave those to “future work” together with the mass of details that we must leave out about the paradigms/styles we do cover:

- **Procedural programming**: the idea of composing a program out of functions operating on arguments. Examples are libraries of mathematical functions, such as `sqrt()` and `cos()`. C++ supports this style of programming through the notion of functions (Chapter 8). The ability to choose to pass arguments by value, by reference, and by `const` reference can be most valuable. Often, data is organized into data structures represented as **structs**. Explicit abstraction mechanisms (such as private data members or member functions of a class) are not used. Note that this style of programming and functions is an integral part of every other style.

- **Data abstraction**: the idea of first providing a set of types suitable for an application area and then writing the program using those. Matrices provide a classic example (§24.36). Explicit data hiding (e.g., the use of private data members of a class) is heavily used. The standard **string** and **vector** are popular examples, which show the strong relationship between data abstraction and parameterization as used by generic programming. This is called "abstraction" because a type is used through an interface, rather than by directly accessing its implementation.

- **Object-oriented programming**: the idea of organizing types into hierarchies to express their relationships directly in code. The classic example is the **Shape** hierarchy from Chapter 14. This is obviously valuable when the types really have fundamental hierarchical relationships. However, there has been a strong tendency to overuse that is, people built hierarchies of types that do not belong together for fundamental reasons. When people derive, ask why. What is being expressed? How does the base/derived distinction help me in this particular case?

- **Generic programming**: the idea of taking concrete algorithms and "lifting" them to a higher level of abstraction by adding parameters to express what can be varied without changing the essence of an algorithm. The high() example from Chapter 20 is a simple example of lifting. The **find()** and **sort()** algorithms from the STL are classic algorithms expressed in very general forms using generic programming. See Chapters 20-21 and the following example.

All together now! Often, people talk about programming styles ("paradigms") as if they were simple disjointed alternatives: either you use generic programming or you use object-oriented programming. If your aim is to express solutions to problems in the best possible way, you will use a combination of styles. By "best" we mean easy to read, easy to write, easy to maintain, and sufficiently efficient. Consider an example: the classic "**Shape** example" originated with Simula (§22.2.4) and is usually seen as an example of object-oriented programming. A first solution might look like this:

```cpp
void draw_all(vector<Shape*&> v)
{
    for(int i = 0; i<v.size(); ++i) v[i]->draw();
}
```

This does indeed look “rather object-oriented.” It critically relies on a class hierarchy and on the virtual function call finding the right `draw()` function for every given `Shape`; that is, for a `Circle`, it calls `Circle::draw()` and for an `Open_polyline`, it calls `Open_polyline::draw()`. But the `vector<Shape*>` is basically a generic programming construct: it relies on a parameter (the element type) that is resolved at compile time. We could emphasize that by using a simple standard library algorithm to express the iteration over all elements:

```cpp
void draw_all(vector<Shape>*& v)
{
    for_each(v.begin(),v.end(),mem_fun(&Shape::draw));
}
```

The third argument of `for_each()` is a function to be called for each element of the sequence specified by the first two arguments (§B.5.1). Now, that third function call is assumed to be an ordinary function (or a functor object) called using the `f(x)` syntax, rather than a member function called by the `p->f()` syntax. So, we use the standard library function `mem_fun()` (§B.6.2) to say that we really want to call a member function (the virtual function `Shape::draw()`). The point is that `for_each()` and `mem_fun()`, being templates, really aren’t very “OO-like”; they clearly belong to what we usually consider generic programming. More interesting still, `mem_fun()` is a freestanding (template) function returning a class object. In other words, it can easily be classified as plain data abstraction (no inheritance) or even procedural programming (no data hiding). So, we could say that this one line of code uses key aspects of all of the four fundamental styles supported by C++.

But why would we write the second version of the “draw all `Shapes`” example? It fundamentally does the same thing as the first version; it even takes a few more characters to write it in that way! We could argue that expressing the loop using `for_each()` is “more obvious and less error-prone” than writing out the `for`-loop, but for many that’s not a terribly convincing argument. A better one is that “`for_each()` says what is to be done (iterate over a sequence) rather than how it is to be done.” However, for most people the convincing argument is simply that “it’s useful”: it points the way to a generalization (in the best generic programming tradition) that allows us to solve more problems. Why are the shapes in a `vector`? Why not a `list`? Why not a general sequence? So we can write a third (and more general) version:

```cpp
template<typename Iter> void draw_all(Iter b, Iter e)
{
    for_each(b,e,mem_fun(&Shape::draw));
}
```

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_849_0.png)
