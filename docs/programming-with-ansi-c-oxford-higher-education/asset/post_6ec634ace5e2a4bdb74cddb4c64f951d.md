
The output confirms that `sort()` delivers what is asked from it. It takes two arguments and both are iterators of the same type. In this program, both are deque iterators in the first case and vector iterators in the second case. It is important to note that `sort()` requires a different type of iterators than `find()` and `copy()`. It requires random access iterators, which are provided by both vector and deque. A list provides only bidirectional iterators and not random access iterators; hence, it cannot work with `sort()`. A statement such as the following where `ls` is a list produces runtime error.

```cpp
sort(ls.begin(), ls.end()) // Erroneous statement
```

## Notes

1. If ever it is required to sort the list elements, one can use a member function of list; for example, it is possible for `ls` to call `ls.sort()`.

2. By default, `sort()` provides the result in an ascending order. It is possible to change the default behaviour by providing a third argument, which is a function object; it is an object of the class with the `()` operator overloaded. A function object with the return value `bool` is known as a predicate object.

Exhibit 16.4 describes allocators.

## Exhibit 16.4 Allocators

Containers can grow and shrink as and when required. For automating this dynamic growth, STL has predefined default memory allocation and deallocation mechanism for all the containers and the types of elements. In most of the cases, the default mechanism is good enough.

Allocators are memory management mechanisms. By default, a default allocator is used with the containers. The call `vector <int>` is actually `vector <int, allocator <int>>` where the second argument `allocator <int>` determines the memory allocation mechanism for int vectors as default. Some other allocators can be passed if the programmers want to manage the memory themselves.

## RECAPITULATION

- The Standard Template Library (STL) is different from other libraries.
- STL contains containers, which in turn contain other objects within, and algorithms, which operate on containers to do some job.
- Iterators are pointer-like devices that help us in connecting the containers and the algorithms.
- STL-based design follows the concept of object-based programming rather than object-oriented programming.
- Generic programming is a mechanism for designing generic software components and algorithms such that maximum amount of reusability is achieved with maximum efficiency.
- The generic software components used in STL are called containers as they are able to contain other objects within themselves.
- Containers are of two types. The first type, known as sequence containers, is able to hold elements in the order as inserted. The second type of containers is known as sorted associative containers. They keep themselves sorted irrespective of the insertions and deletions taking place on them.
- Sorted associative containers are also of two types. The first type stores only the keys and the second type stores an element as well with the key.
- Containers that only store keys are of two types—set and map. Both these accept only one instance of key in the data.
- If we want multiple entries, we need to use multi-key versions, namely, multiset and multimap.
- Generic algorithms free the programmer to code the core part without worrying about the routines such as `sort()` and `merge()` that are to be programmed.
- Iterators provide open design such that we are able to access the elements pointed to by them directly using pointer notations.
- Vector, list, and deque can all have arbitrary length and can expand or shrink when needed.
- New algorithms and containers can be added without being really bothered about other containers or algorithms.
- Algorithms such as `find()` work the same for all containers, whereas `sort()` requires random access iterators, which cannot be provided by lists.
- There are containers such as stack and queue, which are implemented in terms of other sequence containers. They are known as adapted containers.

## KEYWORDS

- **Address manipulation approach** This is a pointer-like approach to access elements one by one.
- **Container** This refers to a software component that can contain other objects.
- **Functional approach** This refers to file operations such as `put()` and `get()` in instances where directly reaching the next element is not possible; a specific function is to be called for that purpose.
- **Generic algorithms** Non-member functions that are capable of working with many objects of container type are known as generic algorithms.
- **Generic programming** Programming in a way that

## EXERCISES

### Multiple Choice Questions

1. The generic non-member algorithms can be used ________.
    (a) only with classes
    (b) only inside member functions
    (c) with all containers
    (d) only with generic containers
    (e) None of the above

2. A map can have ________ record(s) with a single key.
    (a) single
    (b) two
    (c) three
    (d) multiple

3. The function mechanism provides ________.
    (a) better readability
    (b) avoidance of complex problems
    (c) Both (a) and (b)

4. The pointer-like approach to access elements one by one is called ________.
    (a) address manipulation approach
    (b) pointer access approach
    (c) reference access approach
    (d) All of the above

5. The storage requirements for STL components is ________.
    (a) static
    (b) fixed
    (c) dynamic
    (d) None of the above

6. STL uses templates to a large extent to make it as ________ as possible.
    (a) independent of type
    (b) dependent of type
    (c) specific
    (d) All of the above

7. In map container, the elements are automatically sorted on the ________ at the time of the insertion.
    (a) key item
    (b) value item
    (c) Both (a) and (b)
    (d) None of the above

8. ________ is the only container where insertion is a constant time operation irrespective of the location.
    (a) List
    (b) Vector
    (c) Queue
    (d) Deque

9. The generic containers and generic algorithms in STL are connected together by ________.
    (a) templates
    (b) classes
    (c) objects
    (d) iterators

10. Function object is ________.
    (a) an object with a function
    (b) a function declaring a local object
    (c) a function using a global object
    (d) an object of a class with ( ) operator overloaded

7. Explain how sequence iterators work.

8. Explain how sorted associative containers work.

9. List the differences between list and vector containers.

10. List a few algorithms other than the ones described in this chapter.

11. List the differences between set and map containers.

### Practical Exercises

1. Write a program to use an employee class and then provide the following:
    (a) Listing of the employee class in the order of their employee ID
    (b) Listing of employees by their name
    (c) Sorting employees by their employee ID
    (d) Finding an employee based on the residence address

2. Write a program to read details about some players and provide the following:
    (a) Data inserted about the player should be sorted by the sport he/she plays and the name of the player at the time of insertion.
    (b) It is possible that a player plays more than one game. This is also to be incorporated in the program.

3. Write a program for students to enrol in college-wide contests. A student registered in one contest cannot be registered in another. The data about the students must be sorted by the contest name and student name.

4. Write a program to register employees for a daily function of some sort. Any employee can register at any time. The listing can be in any order. An employee can prefer to register after any other employee of his/her choice.

5. Write a program to read and generate a sequence of projects that are to be completed. Assume the project to be a string. Whenever a new project is inserted, it must be either at the beginning or at the end.

### Conceptual Exercises

1. What is the difference between STL and other libraries?

2. What is the advantage of using generic algorithms?

3. What is the need for iterators? What is their role in STL?

4. List the different types of containers.

5. What is the need for sorted associative containers? What is the difference between sorted associative containers and sequence containers?

6. What is the advantage of having readymade components?
