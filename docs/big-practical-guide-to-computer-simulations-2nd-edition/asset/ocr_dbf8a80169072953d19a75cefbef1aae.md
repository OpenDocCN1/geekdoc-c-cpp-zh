```
double reject(double y_max, double x0, double x1,
    double (* pdf)(double))
{
    int found;                /* flag if valid number has been found */
    double x,y;               /* random points in [x0,x1]x[0,p_max] */
    found = 0;
    while(!found)             /* loop until number is generated */
    {
        x = x0 + (x1-x0)*drand48();     /* uniformly on [x0,x1] */
        y = y_max *drand48();           /* uniformly in [0,p_max] */
        if(y <= pdf(x))                 /* accept ? */
            found = 1;
    }
    return(x);
}
```

In lines 10-11 the random point, which is uniformly distributed in the box, is generated. Lines 12-13 contain the check whether a point below the pdf curve has been found. The search in the loop (lines 8-14) continues until a random number has been accepted, which is returned in line 15.

# Example 8.3

The rejection method is applied to a pdf, which has density 1 in [0,0.5] and rises linearly from 0 to 4 in [1,1.5]. Everywhere else it is zero. This pdf is realized by the following C function:

```
double pdf(double x)
{
    if ( (x<0)||
        ((x>0.5)&&(x<1))||
        (x>1.5) )
        return(0.0);
    else if((x>0)&&(x<0.5))
        return(1.0);
    else
        return(4.0*(x-1));
}
```

The resulting empirical histogram pdf is shown in Fig. 8.14.

The simple rejection method can always be applied if the probability density is boxed, but it has the drawback that more random numbers have to be generated than can be used: If A = (x1 - x0)/ymax is the area of the box, one has on average to generate 2A auxiliary random numbers to obtain one random number of the desired distribution. If this leads to a