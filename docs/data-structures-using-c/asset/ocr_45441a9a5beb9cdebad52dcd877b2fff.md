# 9 SEARCHING AND SORTING

# OBJECTIVES

After completing this chapter, the reader will be able to understand the following:

+   - Basic search and sort algorithms
+   - Algorithms with respect to time and space complexity
+   - Appropriate algorithms suitable for practical applications

One of the most common and time consuming tasks in computer science is the retrieval of target information from huge data, which needs searching. Searching is the process of finding the location of the target among a list of objects. The two basic search techniques are the following:

+   1. Sequential search
+   2. Binary search

There are certain ways of organizing data, which make the search process more efficient. If the data is kept in a proper order, it is much easier to search. Sorting is a process of organizing data in a certain order to help retrieve it more efficiently.

In this chapter, we shall study searching and sorting methods. We shall also analyse the algorithms in terms of time complexity.

# 9.1 SEARCHING

The process of locating target data is known as searching. Consider a situation where you are trying to get the phone number of your friend from a telephone directory. The telephone directory can be thought of as a table or a file, which is a collection of records. Each record has one or more fields such as name, address, and telephone number. The fields, which are used to distinguish records, are known as keys. While searching, we are asked to find the record which contains information along with the target key. When we think of a telephone directory, the search is usually by name. However, when we try to locate the record corresponding to a given telephone number, the key will be the telephone number.