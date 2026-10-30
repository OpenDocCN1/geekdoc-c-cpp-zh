words, circle i and circle j intersect if and only if:

√(x_i − x_j)² + (y_i − y_j)² ≤ r_i + r_j

Or equivalently (x_i − x_j)² + (y_i − y_j)² ≤ (r_i + r_j)². Thus, in our program we must effectively check whether this condition holds for any possible i, j, where of course i ≠ j.

Here is how we can do this. We will use arrays x, y, r in which we will store the x, y coordinates of the center and the radius of the circles. Specifically, the x coordinate of the center of the ith circle will be stored in x[i], the y coordinate in y[i], and the radius in r[i]. We will then check whether each circle i intersects with a circle j where j>i.

```
int n=5;                 // number of circles. 5 chosen arbitrarily.
float x[n], y[n];        // coordinates of center of each circle.
float r[n];             // radius of each circle.

for(int i=0;i<n;i++)     // read in all data.
    cin >> x[i] >> y[i] >> r[i];

for(int i=0; i<n; i++){  // Find intersections if any.
    for(int j=i+1; j<n; j++){ 
        if(pow(x[i]-x[j],2)+pow(y[i]-y[j],2) <= pow(r[i]+r[j],2))
            // built in function pow(x,y) = x raised to y.
            cout << "Circles " << i << " and " << j << " intersect." <<endl;
    }
}
```

Thus in the first iteration of the outer for loop, we check for intersections between circle 0 and 1,2,3,...,n−1. In the second iteration, we check for intersections between circle 1 and circles 2,3,...,n−1, and so on. Is this clear that we check all pairs of circles in this process? Consider the kth circle and the lth circle, k ≠ l. Can we be sure that the intersection between them is checked? Clearly, if k < l, then in the iteration of the outer for loop in which i takes the value k, we will check intersections with circles k + 1, k + 2,...,n − 1. This sequence will contain l because k < l. Alternatively, suppose l < k. Then consider the iteration of the outer for loop in which i = l. In this iteration we will check the intersection of circle l with circles l + 1,...,n − 1. Clearly k will be in this sequence because l < k. Thus in either case we will check the intersection between circle k and circle l, for every k,l.

# 13.3 The inside story

We now discuss some details regarding arrays and array accesses. This will specially be useful for understanding how we define functions for operating on arrays. To make the discussion more concrete, suppose we have the following definitions.

```
int p=5, q[5]={11,12,13,14,15}, r=9;
float s[10];
```