The initializer must not have more values than there are elements in the array; otherwise, the statement won’t compile. There can be fewer values in the list, however, in which case the elements for which no initial value has been supplied will be initialized with 0 (false for an array of bool elements). Here’s an example:

```
```cpp
unsigned int height[6] {26, 37, 47};      // Element values: 26 37 47 0 0 0
```
```

The first three elements will have the values that appear in the list. The last three will be 0. To initialize all the elements with 0, you can just use an empty initializer:

```
```cpp
unsigned int height[6] {};      // All elements 0
```
```

To define an array of values that cannot be modified, you simply add the keyword const to its type. The following defines an array of six unsigned int constants:

```
```cpp
const unsigned int height[6] {26, 37, 47, 55, 62, 75}
```
```

Any modification to either one of these six array elements (be it an assignment, increment, or any other modification) will now be prevented by the compiler.

Array elements participate in arithmetic expressions like other variables. You could sum the first three elements of height like this:

```
```cpp
unsigned int sum {};
sum = height[0] + height[1] + height[2];    // The sum of three elements
```
```

You use references to individual array elements such as ordinary integer variables in an expression. As you saw earlier, an array element can be on the left of an assignment to set a new value, so you can copy the value of one element to another in an assignment, like this:

```
```cpp
height[3] = height[2];      // Copy 3rd element value to 4th element
```
```

However, you can’t copy all the element values from one array to the elements of another in an assignment. You can operate only on individual elements. To copy the values of one array to another, you must copy the values one at a time. What you need is a loop.

# ## Understanding Loops

A *loop* is a mechanism that enables you to execute a statement or block of statements repeatedly until a particular condition is met. Two essential elements make up a loop: the statement or block of statements that is to be executed repeatedly forms the so-called *body* of the loop, and a *loop condition* of some kind that determines when to stop repeating the loop. A single execution of a loop’s body is called an *iteration*.

A loop condition can take different forms to provide different ways of controlling the loop. For example, a loop condition can do the following:

+   - Execute a loop a given number of times
+   - Execute a loop until a given value exceeds another value
+   - Execute a loop until a particular character is entered from the keyboard
+   - Execute a loop for each element in a collection of elements