Alternatively, like in a shell script, you can write in the first name #! followed by the complete path name of the Python interpreter.³ This is done in the following example, which we use to introduce some of the main Python concepts:

| GET SOURCE CODE |
|---| 
| DIR: scripts |
| FILE(S): loop.py |

```
1 #!/usr/bin/python
2 
3 a=[12, 45, 98, 112, 114, 135, 167, 298, 312]
4 counter=0
5 for value in a:
6     counter=counter+value
7 print value
8 print "sum of", len(a), "elements:", counter
9 print range(7,12)
10 print a[1], a[2:6]
11 a.insert(3,77)
12 print a
13 a.extend([22, 8])
14 print a
15 a.sort()
16 print a
```

In line 3 of this script, a list is created, one of the basic data types in Python. A list is a linearly ordered sequence of objects, for details see Sec. 6.6. The members of the list are given in square brackets, separated by commas. Python allows several commands in a line, separated by semicolons. In contrast to C, a line does not have to be terminated by a semicolon, instead the line end identifies the end of a command as well. It is very important to note that in contrast to C, variables are not declared. This allows also for mixed types, i.e., the list may contain at the same time integers, floating points, strings, and even other lists as elements. Variables exist after they are created and initialized, until the end of the script or until the same variable name is used for something else. Thus, the variable counter initialized in line 4 will store integer variables. If one writes instead counter=0.0 it would hold floating point variables.

In lines 5-7 a for loop is performed. A for loop is always iterated over the elements of a list (or a string). The body of the loop follows after the colon. In contrast to C, no brackets are used to define the body of the loop. Instead, the body of the loop is identified via indentation: The first line after the for statement belongs to the loop and must be indented by at

³You must make the script executable via chmod +x loop.py in this case.