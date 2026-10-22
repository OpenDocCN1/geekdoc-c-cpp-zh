```
= (16<81) ? Sqrt<16,1,8>::value
: Sqrt<16,9,16>::value
= Sqrt<16,1,8>::value
```

Thus, the result is computed as Sqrt<16,1,8>::value, which is expanded as follows: Click here to view code image

```
mid = (1+8+1)/2
= 5
value = (16<5*5) ? Sqrt<16,1,4>::value
: Sqrt<16,5,8>::value
= (16<25) ? Sqrt<16,1,4>::value
: Sqrt<16,5,8>::value
= Sqrt<16,1,4>::value
```

Similarly, Sqrt<16,1,4>::value is decomposed as follows: Click here to view code image

```
mid = (1+4+1)/2
= 3
value = (16<3*3) ? Sqrt<16,1,2>::value
: Sqrt<16,3,4>::value
= (16<9) ? Sqrt<16,1,2>::value
: Sqrt<16,3,4>::value
= Sqrt<16,3,4>::value
```

Finally, Sqrt<16,3,4>::value results in the following: Click here to view code image

```
mid = (3+4+1)/2
= 4
value = (16<4*4) ? Sqrt<16,3,3>::value
: Sqrt<16,4,4>::value
= (16<16) ? Sqrt<16,3,3>::value
: Sqrt<16,4,4>::value
= Sqrt<16,4,4>::value
```

and Sqrt<16,4,4>::value ends the recursive process because it matches the explicit specialization that catches equal high and low bounds. The final result is therefore value = 4

# 23.3.1 Tracking All Instantiations

Our analysis above followed the significant instantiations that compute the square root of 16. However, when a compiler evaluates the expression Click here to view code image

```
(16<=8*8) ? Sqrt<16,1,8>::value
```