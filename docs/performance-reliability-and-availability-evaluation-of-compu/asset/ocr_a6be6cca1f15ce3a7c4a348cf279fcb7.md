# Performance Measuring 357

# Algorithm 2 Measuring the Duration of Functions in Python Programs

+   1: import time
2: import pstats
3: import math
4: # importing NumPy for matrix operations
5: import numpy
6: #

```
7: def trig(a):
    print("Trigonometric Functions,", end="\n*2")
    print("The converted value from radians to degrees is :", end="\n")
    print(math.degrees(a))
    print("The value of pi/6 is :", end="\n")
    print(math.sin(a))
    print("The value of cosine of pi/6 is :", end="\n")
    print(math.cos(a))
    print("The value of tangent of pi/6 is :", end="\n")
    print(math.tan(a),\n*2)
```

```
18: def factorial(x):
    # This is a recursive function to find the factorial of an integer
    if x == 1:
        return 1
    else:
        return (x * factorial(x-1))
```

```
25: def matrixops(x,y):
    print("The element square root of is :")
    print(numpy.sqrt(x))
    print("The summation of all matrix element is :")
    print(numpy.sum(y))
    print("The column wise summation of all matrix is :")
    print(numpy.sum(x,axis=0))
    print("The row wise summation of all matrix is :")
    print(numpy.sum(y,axis=1))
    print("The transpose of given matrix is :")
    print(x.T,\n*2)
```

```
37: def main():
    rad = math.pi/6
    num = 50
    # initializing matrices
    b = numpy.array([[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12], [13, 14, 15, 16]])
    c = numpy.array([[17, 18, 19, 20], [21, 22, 23, 24], [25, 26, 27, 28], [29, 30, 31, 32]])
    start = time.time()
    trig(rad)
    print("trig(rad) function takes,\ end-start, "seconds", "\n*2")
    start = time.time()
    factorial(num)
    end = time.time()
    print("The factorial of", num, "is", factorial(num),"\n*2")
    print("factorial(num) function takes", end-start, "seconds", "\n*2")
    start = time.time()
    matrixops(b,c)
    end = time.time()
    print("matrixops(x,y) function takes", end-start, "seconds", "\n*2")
if __name__ == "__main__":
    main()
```