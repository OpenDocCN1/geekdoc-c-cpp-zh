# 404 DATA STRUCTURES IN C++

```
}
  return 0;
}
```

A CMS object is created with a seed value of 123 for the random number generator, 29 hash functions and 307 bins/slots for the hashed keys. An ifstream object is created for the newWords.txt file and the readData method is called with that object as its argument. After closing the input stream, the frequency array B will persist and we are given the option of asking about the frequencies of specific words that may be of interest.
Example of results from running the program

```
6866 696
13972 14240
20955 21384
28023 28587
35004 35720
41981 42864
49053 50075
56189 57365
```

The word of interest? the
Estimated frequency is 63135
The word of interest? of
Estimated frequency is 30063

The actual frequency of "the" over all 878,717 words in newWords.txt is 61,847 while the sketch is 63,135. the estimated frequency of "of" over all 878,717 words is found to be 30,063 its actual frequency is 29,391. Table 10.1 reports the results from similar queries for the eight most frequent words in newWords.txt. Both the true and estimated queries are listed in the table.

Table 10.1 Actual versus estimated word frequency
Estimated frequency

| Word | Actual frequency | Estimated frequency |
|---|---|--|
| the | 61847 | 63135 |
| of | 29391 | 30063 |
| and | 26817 | 27829 |
| to | 25627 | 28481 |
| a | 21626 | 25916 |
| in | 18214 | 20074 |
| is | 9982 | 10450 |
| was | 9236 | 10098 |

# 10.3.2 Flexible data input

Section 3.10 using a template approach to create classes for input of general types of numerical data. While this is satisfactory in many cases, there are limitations to its utility. Specifically, it will not work in cases where the structure of the input file is unknown. Thus, one must know priori number of rows and columns in the file, and if there are rows of uneven length, the code must be altered and tailored to work with whatever pattern may exist.

With the vector class in hand, we are now in a position to create a general file input scheme that allows us to read in a file of numeric (or more general types of) data with