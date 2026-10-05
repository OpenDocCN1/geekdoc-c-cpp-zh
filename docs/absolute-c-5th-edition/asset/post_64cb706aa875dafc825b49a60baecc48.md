
the items in the iterator interval can be located in any container, including in an array. Build the vector and list using the array name for the begin iterator and the name + array length as the end iterator for the constructor arguments. Use the modifying algorithm remove (Display 19.19) to remove from the list and the vector elements equal to 4.0 (or the value you duplicated in the array). Display the contents of the vector and list and explain the results.

c. Modify the code part b to assign to iterator variable of appropriate type the iterator returned by the call to the remove generic function. Review the documentation for remove to be certain what these iterator values mean. Output the contents of the array, the vector and the list, begin() to end(), using the "begin" and "end" we described previously for the array. Output the contents of the two containers containing the iterator returned from remove to the end() of each container. Explain your results.

3. A prime number is an integer greater than 1 and divisible only by itself and 1. An integer x is divisible by any integer z such as x=yz. The Greek mathematician Eratosthenes (pronounced Er-tos-nees) gave an algorithm for finding all prime numbers less than N. This algorithm is called the Sieve of Eratosthenes. It works like this: Begin with a list of integers 2 through N. The second is the first (It is important to consider why this is true). The multiples of 2—that is, 4, 6, 8, etc.—are not prime. We cross off the list. The first number after 2 was not crossed, which is 3, is the next prime. The multiples of 3 are not prime. Cross off the list. Note that 6 is already gone, cross off 9, cross off 15, etc. The first number not crossed off is the next prime. The algorithm continues on this fashion until we reach N. All numbers not crossed off are the primes.

a. Write a program using this algorithm to find all primes less than a user-supplied N. Use a vector for the integers. Use an array of bool set to true to keep track of crossed off integers. Change the entry to false for integers that are crossed off the list.

b. Test for N=10, 30, 100, and 300.

Improvements:

c. Actually, we do not need to go all the way to N. You can stop at N/2. Try this test your program. N/2 works and is not the smallest we could use. Argue to get all the primes between 1 and the minimum is the square root of N.

d. Modify your code from part a to use the square root of N as an upper limit.

3. Suppose you have a collection of student records. The records are structures of the following type:

```
struct StudentInfo {
    string name;
    int grade;
};
```

# Programming Projects 907

The records are maintained in a vector<StudentInfo>. Write a program that prompts for fetches data and builds a vector of student records, sorts the vector by name, calculates the maximum and minimum grades, and the class average, then prints this summarizing data along with a class roll. (We are not interested in who had the maximum and minimum grade, and average statistics.) Test your program.

- 5. Continuing Programming 19.4, write a function that separates the students in the vector of StudentInfo into two vectors, one containing records of passing students and one containing records of failing students. (Use a grade of 60 or better passing.)

You are asked to do this in two ways, and to give some run-time estimates.

- a. Continuing to use a vector. You could generate a second vector of passing students and a third vector of failing students. This keeps duplicate records for at least some of the time, so do not it that way. You could create a vector of failing students and a test-for-failing function. You push_back failing student records, then erase (which is a member function) the failing student records from the original vector. Write the program this way.

- b. Consider the efficiency of this solution. You are potentially erasing O(N) members from the middle of the vector. You have to move lot of members in erase from the middle of a vector is an O(N) operation. Give a big-O estimate of the running time for this program. 

- c. If you use a list<StudentInfo>, what is the run time for the erase and insert functions? Consider how the efficiency of erase for a list affects the runtime for the program. Rewrite this program using a list instead of a vector. Remember that a list provides neither indexing nor random access, and its iterators are only bidirectional, not random access.

- a. Here is pseudocode for a program that inputs a value v from the user and then inserts n random numbers, ensuring that there are no duplicates:

```
Input n from user
Create vector v of type int
Loop i = 1 to n
r = random integer between 0 and n-1
Linearly search through value r\if r is not in vector v then add r to the end of v
End Loop
Print out number of elements added to v
```

Implement this program with your linear search routine and add wrapper code that times how long it takes to run. Test the program for different values of n. Depending on the speed of your system, you may need to input large values for n so that the program takes at least one second to run. Here is a sample that indicates how to calculate the difference in time: (time.h is a library that should be available on your version of C++).

# 908 CHAPTER 19 Standard Template Library

```
#include <time.h>

time_t start,end;
double diff;

time(&start); // Record start time
// Rest of program goes here.
time(&end); // Record end time
diff = difftime(end, start);
cout << " It took " << diff << " seconds to execute. " << endl;
```

- b. Create a new program that has the same behavior except that it uses an STL to store the numbers inside a vector:
Input n user
Create s set of type int
Loop i = 1 to n
r = random integer 0 to n-1
Use s.find(r) to search if r is already in the set\if r is not in s then add r to s
End Loop
Print out number of elements added to s

Time your program with the same values of n that you used in the vector version. If the results tell you about the Big-O run time of the find() function for the set compared with linear search through the vector? Note that the find( ) function is really redundant because insert has no effect on the element is already in the set.

- 7. Modify your program from part 19.6 so that the find function is used to search for existing value.

- 8. Information retrieval is concerned with finding relevant documents based on a query. For example, given a set of keywords, a search engine retrieves pages and displays them in order. A simple way to make this comparison is to compute the binary coefficient. The coefficient is a value between 0 and 1, where 1 indicates that the query is very similar to the document and 0 indicates that the query has no common. For example, consider the following sample document:

"Cows are big. Cows go."

# Programming Projects

This document would be parsed into keywords where case is ignored and punctuation discarded into the set containing “cows, are, big, go”.

Once we have a query Q represented as a set of words and a document D represented as a set of words, the similarity between the query and document is computed by

```
$Sim = \frac{|Q \cap D|}{\sqrt{|Q||D|}}$
```

For example, if $D = \{cows, arc, big, go, i, love\}$ and $Q = \{love, holstein, cows\}$

```
$Sim = \frac{\{|love, cows\|}{\sqrt{3}\sqrt{7}} = 0.436$
```

Write a program that allows the user to input a set of strings that represents a document and a set of strings that represents a query. If you are more ambitious, you could write a program that parses an text file and computes the set of unique strings. Represent the document and query as an STL of strings. Then compute and print the similarity between the query and document using the binary coefficient. The `sqrt` function is in `cmath`. Use the generic `set_intersection` function to compute the intersection of $Q$ and $D$.

Here is an example of `set_intersection` to intersect A with B and store the result in C, where all are sets of strings:

```
#include <iterator>
#include <algorithm>
#include <set>
#include <string>

using std::insert_iterator;

set<string> A, B, C;
// Code below assumes strings have been inserted into A and B
insert_iterator<set<string>::iterator> citerator(C.begin(), C.end());
nset_intersection(A.begin(), A.end(), B.begin(), B.end(), citerator);

// set C now contains the intersection of A and B
```

- 9. Re-do or for the first time Programming Project 5.8 in Chapter 5. This project asks you to approximate through simulation the probability that two or more people in the same room have the same birthday, for to fifty people in the room.
