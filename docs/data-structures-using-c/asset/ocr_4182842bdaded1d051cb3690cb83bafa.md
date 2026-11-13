+   4. Print Result
+   5. Stop

Here FACT is the subalgorithm to compute the factorial of a number as

n! = n x (n - 1) x (n - 2) x ... x 1

# SUBALGORITHM FACT

```
1.Read n
2.Let Result = 1
3.while( not equal to 1) do
   Result = Result x n
   n = n - 1
 end while
4.Return Result
```

Note that the subalgorithm makes the algorithm readable and compact. A readable algorithm is the one that, at one glance, gives the reader knowledge about the overall computation process. A compact algorithm is without redundant code. You must have noted in this algorithm that the factorial computation is required twice. A subalgorithm FACT has avoided the redundancy of code to make the algorithm a compact one.

# 1.7 RELATIONSHIP AMONG DATA, DATA STRUCTURES, AND ALGORITHMS

There is an intimate relationship between the structuring of data and analysis of algorithms. In fact, a data structure and an algorithm should be thought of as one single unit; neither one making sense without the other. Let us consider the example of searching for a person’s phone number in a directory. The procedure we follow to search a person and get his/her phone number critically depends on how the phone number and names are arranged in the directory. Let us consider two ways of organizing the data (phone numbers and names) in the directory.

+   1. The data is organized randomly. Then to search a person by name, one has to linearly start from the first name till the last name in the directory. There is no other option.

+   2. If the data is organized by sorting the names (alphabetically sorted in ascending order), then the search is much easier. Instead of linearly searching through all records, one may search in a particular area for particular alphabets, similar to using a dictionary.

As a data is in sorted order, both the binary search and a typical directory search methods work. Hence our ideas for algorithms become possible when we realize that we can organize the data as we wish. We can say that there is a strong relationship between the