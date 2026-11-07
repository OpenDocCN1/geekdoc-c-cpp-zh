```
```cpp
// push elements onto priorities
priorities.push(3.2);
priorities.push(9.8);
priorities.push(5.4);

cout << "Popping from priorities: ";

// pop element from priority_queue
while (!priorities.empty())
{
    cout << priorities.top() << " "; // view top element
    priorities.pop(); // remove top element
} // end while

cout << endl;
} // end main
```
```

Popping from priorities: 9.8 5.4 3.2

**Fig. 22.25** | Standard Library priority_queue adapter class. (Part 2 of 2.)

# 22.8 Algorithms

Until the STL, class libraries of containers and algorithms were essentially incompatible among vendors. Early container libraries generally used inheritance and polymorphism, with the associated overhead of *virtual function calls*. Early libraries built the algorithms into the container classes as class behaviors. The STL separates the algorithms from the containers. This makes it much easier to add new algorithms. With the STL, the elements of containers are accessed through iterators. The next several subsections demonstrate many of the STL algorithms.

> **Performance Tip 22.19**
> 
> *The STL is implemented for efficiency. It avoids the overhead of virtual function calls.*

![](bbox=[0.16, 0.638, 0.216, 0.68])

> **Software Engineering Observation 22.7**
> 
> *STL algorithms do not depend on the implementation details of the containers on which they operate. As long as the container’s (or array’s) iterators satisfy the requirements of the algorithm, STL algorithms can work on C-style, pointer-based arrays, on STL containers and on user-defined data structures.*

![](bbox=[0.16, 0.71, 0.216, 0.777])

> **Software Engineering Observation 22.8**
> 
> *Algorithms can be added easily to the STL without modifying the container classes.*

![](bbox=[0.16, 0.812, 0.216, 0.85])

# 22.8.1 fill, fill_n, generate and generate_n

Figure 22.26 demonstrates algorithms fill, fill_n, generate and generate_n. Functions fill and fill_n set every element in a range of container elements to a specific value. Func-