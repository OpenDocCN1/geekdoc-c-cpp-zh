
16. If 'A' is in s, then s.find('A') returns an iterator located at the element 'A'. If 'A' is not in s, then s.find('A') returns s.end().

17. Just note that $aN+b \leq (a+b)N$, as long as $1 \leq N$.

18. This is mathematics, not C++, so = will mean *equals* not assignment.

First note that $\log_a N=(\log_a b)(\log_b N)$.

To see this first identity, just note that if you raise $a$ to the power $\log_a N$, you get $N$, and if you raise $a$ to the power $(\log_a b)(\log_b N)$, you also get $N$.

If you set $c=(\log_a b)$, you get $\log_a N=c(\log_b N)$.

19. The programs should run exactly the same.

```
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using std::cout;
using std::vector;
using std::search;
...
vector<int> target;
target.push_back(42);
target.push_back(43);
vector<int>::const_iterator result = search(v.begin(), v.end(),
                                            target.begin(), target.end());
if (result != v.end())
    cout << "Found 42, 43.\n";
else
    cout << "42, 43 not there.\n";
```
```

21. No, you must have random access iterators, and the list template class has only bidirectional iterators.

22. Yes, a random access iterator is also a forward iterator.

23. The set_union template function requires that the containers keep their elements in sorted order to allow the function template to be implemented in a more efficient way.

## PRACTICE PROGRAMS

*Practice Programs* can generally be solved with a short program that directly applies the programming principles presented in this chapter.

+   1. Write a program in which you declare a deque to store values of type *double*, read in ten *double* numbers, and store them in the deque. Then call
the generic sort function to sort the numbers in the deque and display the results.

2. Write a program that uses the map template class to compute a histogram of positive numbers entered by the user. The map’s key should be the number that is entered, and the value should be a counter of the number of times the key has been entered so far. Use –1 as a sentinel value to signal the end of user input. For example, if the user inputs:

```
5
12
3
5
5
3
21
-1
```

then the program should output the following (not necessarily in this order):

```
The number 3 occurs 2 times.
The number 5 occurs 3 times.
The number 12 occurs 1 times.
The number 21 occurs 1 times.
```

3. Given a variable of type string set to arbitrary text, write a program that uses the stack template class of type char to reverse the string.

4. Write a function called normalizeArray. Your function should accept a reference to a C++11 style std::array containing 3 double values. Your function should then normalize the array such that the sum of all the elements is 1. Your function should use an iterator to work through the array – first to calculate the sum of all the elements and then to modify the value of each element in the normalization process. Write a driver program to test your function.

## PROGRAMMING PROJECTS

*Programming Projects require more problem-solving than Practice Programs and can usually be solved many different ways. Visit www.myprogramminglab.com to complete many of these Programming Projects online and get instant feedback.*

+   1. Write a program that allows the user to enter any number of student names and their scores. The program should then display the student names and scores according to the ascending order of scores. Use the template class vector and the generic sort function from the STL. Note that you will need to define a structure or class type for data consisting of one student name and score. You will also need to overload the < operator for this structure or class.

+   2. Consider a class representing a text document. This text document may exist in memory as long as a User class has ownership over the text document object. A shared document may be owned by multiple User class objects.
   
   Write a program which contains a User class that stores a collection of shared pointers to Document objects. The Document class should be a simple wrapper around a String object.
   
   Write a test program that creates a number of User objects. A User object should then be able to create a Document object and share this Document object with other User objects through a shared_ptr.
   
   For each User, you should be able to print the documents that the User has ownership over. A User should also be able to give up ownership of a document and this should not affect the other Users. Your test program should also delete a number of Users and show that the documents with shared owners still exist.
   
   Finally, the shared_ptr member function use_count() is useful to show how many owners a particular shared_ptr object has and can be useful for debugging.

+   3. Suppose you have a collection of student records. The records are structures of the following type:

```
struct StudentInfo
{
    string name;
    int grade;
};
```

The records are maintained in a vector<StudentInfo>. Write a program that prompts for and fetches data and builds a vector of student records, then sorts the vector by name, calculates the maximum and minimum grades and the class average, then prints this summarizing data along with a class roll with grades. (We aren’t interested in who had the maximum and minimum grade, though, just the maximum, minimum, and average statistics.) Test your program.

4. Continuing Programming Project 3, write a function that separates the students in the vector of StudentInfo records into two vectors, one containing records of passing students and one containing records of failing students. (Use a grade of 60 or better for passing.)

You are asked to do this in two ways, and to give some run-time estimates.

+   a. Consider continuing to use a vector. You could generate a second vector of passing students and a third vector of failing students. This keeps duplicate records for at least some of the time, so don’t do it that way. You could create a vector of failing students and a test-for-failing function. Then you push_back failing student records, then erase (which is a member function) the failing student records from the original vector. Write the program this way.

+   b. Consider the efficiency of this solution. You are potentially erasing O(N) members from the middle of a vector. You have to move a lot of members in this case. erase from the middle of a vector is an O(N) operation. Give a big-O estimate of the running time for this program.

+   c. If you used a list<StudentInfo>, what are the run-times for the erase and insert functions? Consider how the time efficiency of erase for a list affects the run-time for the program. Rewrite this program using a list instead of a vector. Remember that a list provides neither indexing nor random access and its iterators are only bidirectional, not random access.

5. Redo (or do for the first time) Programming Project 9 from Chapter 11, except use the STL set template class instead of your own set class. Use the generic set_intersection function to compute the intersection of Q and D.

Here is an example of set_intersection to intersect set A with B and store the result in C, where all sets are sets of strings:

```
#include <iterator>
#include <set>
#include <string>
...
set<string> C;
// Note space between >> in line below
insert_iterator<set<string> > cIterator(C, C.begin());
set_intersection(A.begin(), A.end(),
                B.begin(),B.end(),
                cIter);
// set C now contains the intersection of A and B
```

6. In this project you are to create a database of books that are stored using a vector. Keep track of the author, title, and publication date of each book. Your program should have a main menu that allows the user to select from the following: (1) Add a book's author, title, and date; (2) Print an alphabetical list of the books sorted by author; and (3) Quit.

You must use a class to hold the data for each book. This class must hold three string fields: one to hold the author's name, one for the publication date, and another to hold the book's title. Store the entire database of books in a vector in which each vector element is a book class object.

To sort the data, use the generic sort function from the <algorithm> library. Note that this requires you to define the < operator to compare two objects of type Book so that the author field from the two books are compared.

A sample of the input/output behavior might look as follows. Your I/O need not look identical, this is just to give you an idea of the functionality.

```
Select from the following choices:
1.            Add new book
2.            Print listing sorted by author
3.            Quit
1
```

```
Enter title:
More Than Human
```

```
Enter author:
Sturgeon, Theodore
```

```
Enter date:
1953
```

```
Select from the following choices:
1.            Add new book
2.            Print listing sorted by author
3.            Quit
1
```

![](img/88b1f375f11336dbd9dac8b1675d0698_1065_0.png)
