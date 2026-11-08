**(Heap Sort)** This chapter also discusses the heap sort algorithm. This algorithm and its related exercises are available at the Web site, *www.course.com/malik/cpp*, accompanying this book.

# PROGRAMMING EXAMPLE: Election Results

![](bbox=[0.028, 0.264, 0.105, 0.345])

The presidential election for the student council of your local university is about to be held. The chair of the election committee wants to computerize the voting and has asked you to write a program to analyze the data and report the results.

The university has four major divisions, and each division has several departments. For the election, the four divisions are labeled as region 1, region 2, region 3, and region 4. Each department in each division handles its own voting and reports the votes received by each candidate to the election committee. The voting is reported in the following form:

```
firstName lastName regionNumber numberOfVotes
```

The election committee wants the output in the following tabular form:

| Candidate Name | Region1 | Region2 | Region3 | Region4 | Total |
|---|---:|---:|---:|---:|---:|
| Sheila Bower | 23 | 70 | 133 | 267 | 493 |
| Danny Dillion | 25 | 71 | 156 | 97 | 349 |
| Lisa Fisher | 110 | 158 | 0 | 0 | 268 |
| Greg Goldy | 75 | 34 | 134 | 0 | 243 |
| Peter Lamba | 285 | 56 | 0 | 46 | 387 |
| Mickey Miller | 112 | 141 | 156 | 67 | 476 |

Winner: Sheila Bower, Votes Received: 493

Total votes polled: 2216

The names of the candidates must be in alphabetical order in the output.

For this program, we assume that six candidates are seeking the student council’s president post. This program can be enhanced to handle any number of candidates.

The data are provided in two files. One file, candData.txt, consists of the names of the candidates seeking the president post. The names of the candidates in this file are in no particular order. In the second file, voteData.txt, each line consists of the voting results in the following form: