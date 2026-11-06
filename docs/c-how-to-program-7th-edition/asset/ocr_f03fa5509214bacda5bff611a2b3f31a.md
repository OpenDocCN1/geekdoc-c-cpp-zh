```
```
Unsorted vector:
   30 47 22 67 79 18 60 78 26 54

split:       30 47 22 67 79 18 60 78 26 54
             30 47 22 67 79
                         18 60 78 26 54

split:       30 47 22 67 79
             30 47 22
                      67 79

split:       30 47 22
             30 47
                22

split:       30 47
             30
                47

merge:       30
             47
             30 47

merge:       30 47
                22
             22 30 47

split:                67 79
                      67
                         79

merge:                67
                      79
                      67 79

merge:       22 30 47
                      67 79
             22 30 47 67 79

split:                      18 60 78 26 54
                            18 60 78
                                     26 54

split:                      18 60 78
                            18 60
                               78

split:                      18 60
                            18
                               60

merge:                      18
                            60
                            18 60

merge:                      18 60
                                  78
                            18 60 78
```
```

**Fig. 19.7** | MergeSort test program. (Part 2 of 3.)