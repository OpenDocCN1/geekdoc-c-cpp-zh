
+   A3: is_partitioned(): determines whether a range is partitioned so that all elements satisfying a unary predicate condition are positioned before all elements not satisfying the predicate. An example is {5,3,9,1,3,2,4,8,2,6} in which odd numbers are segregated from non-odd numbers.

+   A4: partition_point(): returns the position of the first element in the partitioned range.

+   A5: is_heap(): determines if a container is a heap (maximum element first). There are four variants.

+   A6: all_of(), any_of(), none_of(): these algorithms determine whether all, any (at least one) or none of the elements are in a range by applying a unary predicate to them.

Answer the following questions:
a) Consult Josuttis (2012) and the C++ online documentation (for example, www.cppreference.com) to determine how to use algorithms A1 to A6 for simple test cases.
b) Create a vector with different elements. Create a copy and apply std::shuffle() to it. Determine whether the two vectors are permutations of each other.
c) Consider the container {97,88,95,66,55,95,48,66,35,48,55,62,77,25,38,18,40,30,26,24}. Is it a max heap?
d) Consider the container {1,2,3,4,5,6,7,8,9}. Determine what happens when we apply algorithm A6 to this container.

## 3. (for_each() Algorithm and Lambda)

The objective of this exercise is to adapt and extend the code in Section 17.1 in order to gain some experience with STL algorithms.
Answer the following questions:
a) Generalise the free function Modify() in order to remove the hard-wired (magic) number in the code. We wish to be able to scale a container based on a user-supplier number. Implement the new functionality using both a function object and a lambda function with a corresponding captured variable.
b) Test the new functionality using the STL algorithm transform().
c) Compare the relative advantages of free functions, lambda functions and function objects in the current context with regard to code understandability and maintainability.

## 4. (Non-modifying Algorithms)

We include a number of exercises that process STL containers and produce some output, usually a number or a data structure. For convenience, use STL vectors as the input container and note that there are several possible solutions to a given problem, some more efficient and/or readable than others. It is up to you to decide how to design the algorithm and the structure/type of the output.
a) Count the frequency of each value in a container. For example, for {1,2,4,5,4,1} we get the output {{1,2}, {2,1}, {4,2}, {5,1}} as pairs of {value, frequency}. There are different ways to model the output depending on your requirements.
b) Write a function to compute the minimum, maximum, sum and average of the values of the elements in a container with numeric values. The output is a tuple with four elements.
c) Consider the container S = {1,2,-3,4,5,5,6}. Use an STL algorithm to find the first occurrence of the value.

5. Now use the following functions:
std::bind2nd()
std::bind()
Lambda expression
to find the position of the first even number in S.

d) Consider the container S = {1,2,5,5,−3,4,5,5,5,6,3,4,5}. Determine how to do the following:

+   - Return the position of the first three consecutive elements having the value 5.
+   - Return the position of the first element of the first subrange matching {3,4,5}.
+   - Return the position of the first element of the last subrange matching {3,4,5}.

e) Consider the container S = {1,2,5,5,−3,4,5,5,5,6,3,4,5}. Find the first element in S that has a value equal to the value of the following element.

f) Consider the container S = {1,2,5,5,−3,4,5,5,5,6,3,4,5} and S1 = {1,2,5}. Determine whether the elements in S1 are equal to the elements in S.

## 6. (Which Style to Use?)

Some STL algorithms use unary and binary predicates. Both predicate types return a bool. A unary predicate has one input argument while a binary predicate has two input arguments. We can model these predicates and other kinds of functions in a number of ways:

+   - User-defined function objects.
+   - Predefined STL function objects (for example, std::multiplies<T>()).
+   - Using lambda functions (possibly with captured variables).

Answer the following questions:

a) Compare these three solutions with regard to quality issues such as readability, understandability and maintainability.

b) Consider transforming a vector of integers into a set of integers. Only those elements whose absolute value is strictly greater than a given threshold value should appear in the destination. An example is the vector {1,2,1,4,5,5,−1}. If the threshold value is 2 then the output set will be {4,5}. Implement this problem using the three bespoke methods above.

c) Having developed and debugged the code in part b), review the three solutions from the perspective of understandability, maintainability and efficiency.

## 7. (Modifying the Elements of a Container)

We give some exercises on applying the modifying, replacing and removing algorithms in STL. The initial focus is more on functionality and less on efficiency. Most of the exercises use specific examples and it is your task to use them as the test cases for your code.

Answer the following questions.

a) Consider the set S1 = {a,b,c,d,e,k} and the set S2 = {a,e}. Remove those elements from S1 that are not in S2. The output set is {b,c,d,k}.

b) Create a class Point that models two-dimensional points. Provide constructors, member functions to access the coordinates of a point and a member function to compute the distance between two points. Define a binary predicate that tests two points for equality (they have the same values for their x and y coordinates). Now create an array of points (duplicates allowed). Transform this array to a set of points with no duplicates. Finally, filter this set (that is, remove points) of those points that are not within a given distance from some predefined point.

**c)** We wish to create functions that process strings in some way (in a sense, we are emulating a simple version of the *Boost C++ String Algorithm* library). A string can be seen as a special kind of vector whose elements are characters. Create functions to do the following (in all cases the input is a string):

+   - Trim all leading and trailing blanks (space, tabs, etc.) from the string.
+   - Trim all leading and trailing blanks based on a unary predicate (e.g. is a digit, is a member of some set of characters).
+   - Produce a vector of strings from a character-separated string.
+   - Join two strings.

## 8. (How Many Ways to Print a Container?)

The objective of this exercise is to focus on the `std::for_each()` algorithm and use it to print the elements of an instance of `std::vector<double>`. We use functionality from C++11 and we attempt to print a vector in as many ways as possible. The advantage is that we can get some hands-on experience with new syntax and we can apply the results to more advanced applications.

Answer the following questions:

+   **a)** Write a function that accepts a vector as argument and that iterates over its elements using standard functionality for STL iterators.
+   
+   **b)** Now apply the `std::for_each()` algorithm to print the elements of the vector. Use a function object and a lambda function as the unary procedure (last argument of the algorithm).
+   
+   **c)** Apply the `std::for_each()` algorithm to modify the values of the elements of the vector. Use both a function object and a lambda function as the *unary procedure* (last argument of algorithm).
+   
+   **d)** Consider using *range-based for* loops to print the elements of the vector:

```
void print(const std::vector<double>& vec)
{
    for (const auto& elem : vec)
    {
        std::cout << elem << ",";
    }
}
```

Consider the functionality for *uniform initialisation* and *initialiser lists* to use to initialise vectors before printing them.

+   **e)** We use the `std::for_each()` algorithm to iterate in a vector and we compute the maximum, minimum and average of the elements in the vector. Use captured variables for these three quantities and encapsulate them as a tuple whose return type is `std::tuple<double, double, double>`.
+   
+   **f)** We generalise the function to print a vector so that it can be used with other sequence containers. To this end, use the *template–template parameter* trick.

*Hint:*

```
template <typename T, template <typename S,typename Alloc >
    class Container,typename TAlloc>
```
