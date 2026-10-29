
+   ■ The main container template classes in the STL are list, which has mutable bidirectional iterators; and the template classes vector and deque, both of which have mutable random-access iterators.

+   ■ stack and queue are container adapter classes, which means they are built on top of other container classes. A stack is a last-in/first-out container. A queue is a first-in/first-out container.

+   ■ The set, map, multiset, and multimap container template classes store their elements in sorted order for efficiency of search algorithms. A set is a simple collection of elements. A map allows storing and retrieving by key values. The multiset class allows repetitions of entries. The multimap class allows a single key to be associated with multiple data items.

+   ■ The STL includes template functions to implement generic algorithms with guarantees on their maximum running time.

## ANSWERS TO SELF-TEST EXERCISES

+   1. v.begin() returns an iterator located at the first element of v. v.end() returns a value that serves as a sentinel value at the end of all the elements of v.

+   2. *p is the dereferencing operator applied to p. *p is a reference to the element at location p.

+   3. using std::vector<int>::iterator;
+   ...
+   iterator p;
+   for (p = v.begin(), p++; p != v.end(); p++)
+       cout << *p << " ";

+   4. D C C

+   5. B C

+   6. Either would work.

+   7. A major difference is that a vector container has random-access iterators, whereas list has only bidirectional iterators.

+   8. All except slist.

+   9. vector and deque.

+   10. They all can have mutable iterators.

+   11. The stack template adapter class has no iterators.

+   12. The queue template adapter class has no iterators.

+   13. No value is returned; pop is a void function.

+   14. To facilitate an efficient search for elements.

+   15. Yes, they can be of any type, although there is only one type for each object. The type parameter in the template class is the type of element stored.

16. If 'A' is in s, then s.find('A') returns an iterator located at the element 'A'. If 'A' is not in s, then s.find('A') returns s.end().

17. Just note that aN + b ≤ (a + b)N, as long as 1 ≤ N.

18. This is mathematics, not C++. So, = will mean equals, not assignment.
First note that loga N = (loga b)(logb N).
To see this first identity just note that if you raise a to the power loga N you get N and if you raise a to the power (loga b)(logb N) you also get N.
If you set c = (loga b) you get loga N = c (logb N).

19. The programs should run exactly the same.

```
20. #include <iostream>
#include <vector>
#include <algorithm>
using std::cout;
using std::vector;
using std::vector<int>::const_iterator;
using std::search;
...
vector<int> target;
target.push_back(42);
target.push_back(43);
const_iterator result = search(v.begin(), v.end(),
    target.begin(), target.end());
if (result != v.end())
    cout << "Found 42, 43.\n";
else
    cout << "42, 43 not there.\n";
```

21. No, you must have random-access iterators, and the list template class only has bidirectional iterators.

22. Yes, a random-access iterator is also a forward iterator.

23. The set_union template function requires that the containers keep their elements in sorted order to allow the function template to be implemented in a more efficient way.

## PROGRAMMING PROJECTS

1. The point of this exercise is to demonstrate that: An object that behaves like an iterator is an iterator. More precisely, if an object accesses some container and behaves like an iterator of a particular strength, then that object can be used as an iterator to manipulate the container with any of the generic functions that require an iterator having that strength. However, while the generic algorithms can be used with this container, the member functions, such as begin and end, will (of course) not be present (for example, in an array) unless they have

### 3. A prime number is an integer greater than 1 and divisible only by itself and and 1. An integer x is divisible by an integer y if there is another integer z such x = y*z. The Greek mathematician Eratosthenes (pronounced: Er-ah-thos-then-ez) gave an algorithm for finding all prime numbers less than some integer N. This algorithm is call the Sieve of Eratosthenes. It works like this: Beginning with a list of integers 2 through N, the number 2 is the first prime. (It is instructive to consider why this is true.) The multiples of 2, that is, 4, 6, 8, etc., are not prime. We cross these off the list. Then the first number after 2 that was not crossed off is the next prime. This number is 3. The multiples of 3 are not primes. Cross these off the list. Note that 6 is already gone, cross off 9, 12 is already gone, cross off 15, etc.. The first number not crossed off is the next prime. The algorithm continues on this fashion until we reach N. All the numbers not crossed off the list are primes.

+   a. Write a program using this algorithm to find all primes less than a user supplied number N. Use a vector container for the integers. Use an array of bool initially set to all true to keep track of crossed off integers. Change the entry to false for integers that are crossed off the list.

+   b. Test for N = 10, 30, 100, and 300.

## Improvements:

+   c. Actually, we don’t need to go all the way to N. You can stop at N/2. Try this and test your program. N/2 works and is better, but is not the smallest number we could use. Argue that to get all the primes between 1 and N the minimum limit is the square root of N.

+   d. Modify your code from part a) to use the square root of N as an upper limit.

### 4. Suppose you have a collection of student records. The records are structures of the following type:

```
struct StudentInfo
{
    string name;
    int grade;
};
```

The records are maintained in a vector<StudentInfo>. Write a program that prompts for and fetches data and builds a vector of student records, then sorts the vector by name, calculates the maximum and minimum grades, and the class average, then prints this summarizing data along with a class roll with grades. (We aren’t interested in who had the maximum and minimum grade, though, just the maximum, minimum and average statistics.) Test your program.

### 5. Continuing Programming Project 4, write a function that separates the students in the vector of StudentInfo records into two vectors, one containing records of passing students and one containing records of failing students. (Use a grade of 60 or better for passing)

You are asked to do this in two ways, and to give some runtime estimates.

+   a. Consider continuing to use a vector. You could generate a second vector of passing students and a third vector of failing students. This keeps duplicate records for at least some of the time, so don’t do it that way. You could create a vector of failing students and a test-for-failing function. Then you push_back failing student records, then erase (which is a member function) the failing student records from the original vector. Write the program this way.

+   b. Consider the efficiency of this solution. You are potentially erasing $O(N)$ members from the middle of a vector. You have to move a lot of members in this case. Erase from the middle of a vector is an $O(N)$ operation. Give a big $O$ estimate of the running time for this program.

+   c. If you used a `list<StudentInfo>`, what are the run-time for the erase and insert functions? Consider how the time efficiency of erase for a list affects the runtime for the program. Rewrite this program using a `list` instead of a vector. Remember that a list provides neither indexing nor random access, and its iterators are only bidirectional, not random access.

## 20

## CHAPTER
Patterns and UML

![](img/9505fd46e120aa9c1406715936ff6251_829_0.png)

+   20.1 PATTERNS 848
+   Adapter Pattern 839
+   The Model-View-Controller Pattern 839
+   Example: A Sorting Pattern 841
+   Efficiency of the Sorting Pattern 845
+   Tip: Pragmatics and Patterns 847
+   Pattern Formalism 848
+   
+   20.2 UML 849
+   History of UML 849
+   UML Class Diagrams 850
+   Class Interactions 850
+   
+   CHAPTER SUMMARY 851
+   ANSWERS TO SELF-TEST EXERCISES 851
+   PROGRAMMING PROJECTS 853
