```
```
frequency[ 1 ]++
```
```

which increments the value in array element 1. To evaluate the expression, start with the value in the innermost set of square brackets (answer). Once you know answer's value (which is the value of the loop control variable in line 23), plug it into the expression and evaluate the next outer set of square brackets (i.e., responses[answer], which is a value selected from the responses array in lines 14–17). Then using the resulting value as the subscript for the frequency array to specify which counter to increment.

When answer is 1, responses[answer] is the value of responses[1], which is 2, so the program interprets frequency[responses[answer]]++ as

```
```
frequency[ 2 ]++
```
```

which increments array element 2.

When answer is 2, responses[answer] is the value of responses[2], which is 6, so the program interprets frequency[responses[answer]]++ as

```
```
frequency[ 6 ]++
```
```

which increments array element 6, and so on. Regardless of the number of responses processed in the survey, the program requires only an 11-element array (ignoring element zero) to summarize the results, because all the response values are between 1 and 10 and the subscript values for an 11-element array are 0 through 10.

If the data in responses contained an invalid value, such as 13, the program would have attempted to add 1 to frequency[13], which is outside the bounds of the array. C++ has no array bounds checking to prevent the computer from referring to an element that does not exist. Thus, an executing program can "walk off" either end of an array without warning. You should ensure that all array references remain within the bounds of the array.

![](bbox=[0.13, 0.68, 0.87, 0.74])

![](bbox=[0.13, 0.74, 0.87, 0.81])

![](bbox=[0.13, 0.81, 0.87, 0.89])

C++ is an extensible language. Section 7.11 presents C++ Standard Library class template vector, which enables you to perform many operations that are not available for C++'s built-in arrays. For example, we'll be able to compare vectors directly and assign one vector to another. In Chapter 11, we extend C++ further by implementing an array as a user-defined class of our own. This new array definition will enable us to input and output entire arrays with cin and cout, initialize arrays when they're created and prevent access to out-of-range array elements. We'll even be able to use noninteger subscripts.