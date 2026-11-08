# Chapter 26

# Good Code, 6th Dan: The Right Container
for Each Task

Here I provide a decision aid on which container is right for which task. In the end, I will once again concretely bring together the application of containers and algorithms, because algorithms are part of solving tasks with containers.

# 26.1  All Containers Arranged by Aspects

It is possible to find comprehensive descriptions of the behavior of any given container in a multitude of places. This allows you to select the most appropriate container for a particular scenario “simply” by reading all the documentation.

Or you can read this section, where I do it the other way around: given a scenario or important aspect, and I tell you the strengths and weaknesses of the individual containers for it. Then you can choose the container that fits the given situation.

# 26.1.1  When Is a “vector” Not the Best Choice?

The first rule of thumb is this: use a *vector*. Only if that is not suitable should you use something else.

A *vector* has so many good properties that there must be a good reason to decide against it:

+   - **vector versus array**
+     If you don't want the elements to end up on the heap, but rather be managed on the stack like automatic variables, you can consider an *array*. *array* does not guarantee that the memory is always managed in the same place, but in practice it is very likely to be the stack. Alternatively, you can also use a *vector* with a special allocator.
+   
+   - **vector versus deque**
+     If *push_back* and *pop_back* are not enough when inserting, because you also need *push_front* and *pop_front*, then use deque.
+   
+   - **vector versus list**
+     If a vector grows dynamically, copying elements is expensive or impossible, and you don't know beforehand how many elements will come, then you can switch to *list*. It guarantees that once inserted, elements stay in place. A second reason could be