
## Display 19.14 Program Using the map Template Class (part 2 of 2)

```
Mars - The Red Planet
Mercury - Hot planet
Neptune - 1500 mile-per-hour winds
Pluto - Dwarf planet
Saturn - Has rings
Uranus - Tilts on its side
Venus - Atmosphere of sulfuric acid
```

## TIP: Use Initialization, Ranged for, and auto with Containers

Several features introduced in C++11 make it easier to work with collections. In particular, you can initialize your container objects using the uniform initializer list format, which consists of initial data in curly braces. You can also use auto and the ranged for loop to easily iterate through a container. Consider the following two initialized collection objects:

```
map<int, string> personIDs = {
    {1,"Walt"},
    {2,"Kenrick"}
};
```

```
set<string> colors = {"red","green","blue"};
```

We can iterate conveniently through each container using a ranged for loop and auto:

```
for (auto p : personIDs)
    cout << p.first << " " << p.second << endl;
for (auto p : colors)
    cout << p << " ";
```

The output of these lines is

```
1 Walt
2 Kenrick
blue green red
```

## Self-Test Exercises

- 14. Why are the elements in the set template class stored in sorted order?
- 15. Can a set have elements of a class type?
- 16. Suppose s is of the type set<char>. What value is returned by s.find('A') if 'A' is in s? What value is returned if 'A' is not in s?
- 17. How many elements will be in the map mymap after the following code executes?
  + map<int, string> mymap;
  + mymap[5] = "c++";
  + cout << mymap[4] << endl;

## 19.3 Generic Algorithms

> "And if you take one from three hundred and sixty-five, what remains?"
> "Three hundred and sixty-four, of course."
> Humpty Dumpty looked doubtful. "I'd rather see that done on paper," he said.
> 
> LEWIS CARROLL, Through the Looking-Glass, and What Alice Found There.
> London: Macmillan and Co., 1871

This section covers some basic function templates in the STL. We cannot give you a comprehensive description of them all here, but we will present a large enough sample to give you a good feel for what is contained in the STL and to give you sufficient detail to start using these template functions.

These template functions are sometimes called generic algorithms. The term algorithm is used for a reason. Recall that an algorithm is just a set of instructions for performing a task. An algorithm can be presented in any language, including a programming language like C++. But, when using the word algorithm, programmers typically have in mind a less formal presentation given in English or pseudocode. As such, it is often thought of as an abstraction of the code defining a function. It gives the important details but not the fine details of the coding. The STL specifies certain details about the algorithms underlying the STL template functions, which is why they are sometimes called generic algorithms. These STL function templates do more than just deliver a value in any way that the implementers wish. The function templates in the STL come with minimum requirements that must be satisfied by their implementations if they are to satisfy the standard. In most cases, they must be implemented with a guaranteed running time. This adds an entirely new dimension to the idea of a function interface. In the STL, the interface not only tells a programmer what the function does and how to use the functions, but also how rapidly the task will be done. In some cases, the standard even specifies the particular algorithm that is used, although not the exact details of the coding. Moreover, when it does specify the particular algorithm, it does so because of the known efficiency of the algorithm. The key new point is the specification of an efficiency guarantee for the code. In this chapter, we will use the terms generic algorithm, generic function, and STL function template to all mean the same thing.

In order to have some terminology to discuss the efficiency of these template functions or generic algorithms, we first present some background on how the efficiency of algorithms is usually measured.

generic
algorithm

## Running Times and Big-O Notation

If you ask a programmer how fast his or her program is, you might expect an answer like "two seconds." However, the speed of a program cannot be given by a single number. A program will typically take a longer amount of time on larger inputs than it will on smaller inputs. You would expect that a program for sorting numbers would take less time to sort 10 numbers than it would to sort 1000 numbers. Perhaps it takes 2 seconds to sort 10 numbers, but 10 seconds to sort 1000 numbers. How then should the programmer answer the question "How fast is your program?" The programmer would have to give a table of values showing how long the program takes for different sizes of

input. For example, the table might be as shown in Display 19.15. This table does not give a single time, but instead gives different times for a variety of different input sizes.

The table is a description of what is called a function in mathematics. Just as a (non-void) C++ function takes an argument and returns a value, so too does this function take an argument, which is an input size, and returns a number, which is the time the program takes on an input of that size. If we call this function T, then T(10) is 2 seconds, T(100) is 2.1 seconds, T(1000) is 10 seconds, and T(10,000) is 2.5 minutes. The table is just a sample of some of the values of this function T. The program will take some amount of time on inputs of every size. So although they are not shown in the table, there are also values for T(1), T(2), ..., T(101), T(102), and so forth. For any positive integer N, T(N) is the amount of time it takes for the program to sort N numbers. The function T is called the running time of the program.

So far we have been assuming that this sorting program will take the same amount of time on any list of N numbers. That need not be true. Perhaps it takes much less time if the list is already sorted or almost sorted. In that case, T(N) is defined to be the time taken by the "hardest" list—that is, the time taken on that list of N numbers that makes the program run the longest. This is called the worst-case running time. In this chapter, we will always mean worst-case running time when we give a running time for an algorithm or for some code.

The time taken by a program or algorithm is often given by a formula, such as 4N + 3, 5N + 4, or N². If the running time T(N) is 5N + 5, then on inputs of size N the program will run for 5N + 5 time units.

The following is some code to search an array a with N elements to determine whether a particular value target is in the array:

```
int i = 0;
bool found = false;
while (i < N && !(found))
    if (a[i] == target)
        found = true;
    else
        i++;
```

## Display 19.15 Some Values of a Running Time Function

| Input Size | Running Time |
|---|---|
| 10 numbers | 2 seconds |
| 100 numbers | 2.1 seconds |
| 1000 numbers | 10 seconds |
| 10,000 numbers | 2.5 minutes |

We want to compute some estimate of how long it will take a computer to execute this code. We would like an estimate that does not depend on which computer we use, either because we do not know which computer we will use or because we might use several different computers to run the program at different times.

## CHAPTER 19 Standard Template Library

One possibility is to count the number of “steps,” but it is not easy to decide what a step is. In this situation the normal thing to do is count the number of operations. The term operations is almost as vague as the term step, but there is at least some agreement in practice about what qualifies as an operation. Let us say that, for this C++ code, each application of any of the following will count as an operation: =, <, &&, !, [], ==, and ++. The computer must do other things besides carry out these operations, but these seem to be the main things that it is doing, and we will assume that they account for the bulk of the time needed to run this code. In fact, our analysis of time will assume that everything else takes no time at all and that the total time for our program to run is equal to the time needed to perform these operations. Although this is an idealization that clearly is not completely true, it turns out that this simplifying assumption works well in practice, and so it is often made when analyzing a program or algorithm.

Even with our simplifying assumption, we still must consider two cases: Either the value target is in the array or it is not. Let us first consider the case when target is not in the array. The number of operations performed will depend on the number of array elements searched. The operation = is performed two times before the loop is executed. Since we are assuming that target is not in the array, the loop will be executed N times, one for each element of the array. Each time the loop is executed, the following operations are performed: <, &&, !, [], ==, and ++. This adds five operations for each of N loop iterations. Finally, after N iterations, the Boolean expression is again checked and found to be false. This adds a final three operations (<, &&, !). If we tally all these operations, we get a total of 6N + 5 operations when the target is not in the array. We will leave it as an exercise for the reader to confirm that if the target is in the array, then the number of operations will be 6N + 5 or fewer. Thus, the worst-case running time is T(N) = 6N + 5 operations for any array of N elements and any value of target.

We just determined that the worst-case running time for our search code is 6N + 5 operations. But an operation is not a traditional unit of time, like a nanosecond, second, or minute. If we want to know how long the algorithm will take on some particular computer, we must know how long it takes that computer to perform one operation. If an operation can be performed in one nanosecond, then the time will be 6N + 5 nanoseconds. If an operation can be performed in one second, the time will be 6N + 5 seconds. If we use a slow computer that takes ten seconds to perform an operation, the time will be 60N + 50 seconds. In general, if it takes the computer t nanoseconds to perform one operation, then the actual running time will be approximately t(6N + 5) nanoseconds. (We said approximately because we are making some simplifying assumptions, and therefore the result may not be the absolutely exact running time.) This means that our running time of 6N + 5 is a very crude estimate. To get the running time expressed in nanoseconds, you must multiply by some constant that depends on the particular computer you are using. Our estimate of 6N + 5 is only accurate to within a constant multiple.

Estimates on running time, such as the one we just went through, are normally expressed in something called **big-O notation**. (The O is the letter “Oh,” not the digit zero.) Suppose we estimate the running time to be, say, 6N + 5 operations, and suppose

³Because of short-circuit evaluation, ! {found} is not evaluated, so we actually get two, not three, operations. However, the important thing is to obtain a good upper bound. If we add in one extra operation, that is not significant.
