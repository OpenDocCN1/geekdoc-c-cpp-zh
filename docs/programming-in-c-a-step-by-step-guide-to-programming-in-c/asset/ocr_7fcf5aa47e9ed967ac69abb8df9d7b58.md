```
int positive(int);
float sqr;
if(positive(x)) /* psquare() in turn calls the function positive() */ {
sqr=sqrt(x));
if(sqr-int(sqr))==0)
return 1;
else
return 0;
}
int positive(int m)
{
if(m>0)
return 1;
else return 0;
}
```

Execute the above program and observe the result.

In the above program the main function calls the function psquare() and it in turn calls the function positive() to check whether the number to be checked for perfect square is a positive or not before checking.

The return statement can be absent altogether from a function definition, though this is generally regarded as a poor programming practice. If a function reaches end of the block without encountering a return statement, control simply reverts back to the calling portion of the program without returning any information. Using an empty return statement(without the accompanying expressions) is recommended.