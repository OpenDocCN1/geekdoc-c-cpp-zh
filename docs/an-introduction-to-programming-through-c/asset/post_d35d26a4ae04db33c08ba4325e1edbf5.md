
```
char command; cin >> command;
if(command == 'd'){
    // driver arrives
    if(nWaiting >= n) cout << "Queue full.\n";
    else{
        cin >> driverID[nWaiting];
        nWaiting++;
    }
}
else if(command == 'c'){
    // customer arrives
    if(nWaiting == 0) cout << "Nothing available. Try later.\n";
    else{
        cout << "Assigning " << driverID[0] << endl;
        for(int i=1; i < nWaiting; i++) // shift up waiting drivers
            driverID[i-1] = driverID[i];
        nWaiting--;
    }
}
else if(command == 'x') break;
else cout << "Illegal command.\n";
}
```

Note that we have added checks to see if the array driverID is already full when a driver is to be entered, and to see if there is at least one element in it when a customer arrives.

You might think that perhaps there should be a way to write the program without having to shift up the entries in driverID when we assign the driver at index 0. Instead of moving up the drivers in the array, could we not adjust our notion about where the front of the queue is? Indeed this will work. But it will need a bit more care. To do this right, perhaps it is worth considering how we might have dispatched taxis without computers.

## Dispatching without computers

It is always worth thinking about how any problem, including taxi dispatching, might be solved without computers. Say the dispatcher writes the driverID numbers on a blackboard, top to bottom, as the drivers report. When a driver arrives, we put down the number at the bottom of the list. When a passenger comes in, the number at the top of the list is given to the passenger, and then the number is erased.

For simplicity, let us assume that our blackboard can only hold 100 phone numbers. Managing this space on the blackboard turns out to be slightly tricky. Suppose 60 drivers report, and you write down their numbers, starting at the top. Suppose you next have 50 passengers, so you match them to the top 50 numbers, which you erase. At this point you have only 10 numbers on the board, however, they are not at the top of the board, but they start halfway down the board. Suppose now 60 more drivers report. You would place 40 of these numbers below the 10 you have on the board, and that would take you to the bottom of the board. Where should you place the remaining 20? It is natural to start writing numbers from the top again, as if the bottom of the board were joined to the top. Think of the blackboard as forming the curved surface of a cylinder! Thus at this point, you have 70

![](img/c7233aedab7e4c7cad32a7615b6a4783_225_0.png)

numbers on the board. They begin at position 50 (the topmost position being 0), go to the last position, 99. Then they “wrap around” so that the last 20 numbers occupy positions 0 through 19 on the board. Positions 20–49 are then unused. This should not confuse us; say we make a mark next to the first waiting driver. When we assign a driver, we erase the number from the board, and also shift the mark down one. This works fine so long as the number of taxi drivers waiting at any time does not exceed 100.

## Emulating a blackboard on a computer

Our program will mirror the actions given above. We do not shift drivers up when a driver is assigned, instead we have a variable `front`, which will always contain the index of the element of `driverID` containing the earliest waiting unassigned driver. This performs the function of the mark that the dispatcher places on the board.

If there are `nWaiting` drivers waiting for customers, their IDs will appear at positions starting at `front`. We need to be slightly careful as we say this: how do we describe what happens when the board fills to the bottom and the dispatcher is forced to write the numbers starting at the top again? We would like to somehow say that index that comes “next” after the last index n−1 (i.e. the “bottom” of the board) is index 0 (i.e. the “top” of the board). So instead of saying that the next index after `front` is `front+1`, we will say that it is `(front+1) % n`. If `front` has some value `i<n−1`, then `(front+1) % n` is just `i+1`. However, if `front` equals `n−1`, then `(front+1) % n` will indeed become 0 as we wish. Thus we will simply require that if there are `nWaiting` drivers that are waiting, their IDs will be at indices `front`, `(front + 1) % n`, …, `(front + nWaiting − 1) % n`.

Next we consider what actions to execute when a driver arrives. As before, we accept the ID only if `driverID` is not full. The ID of the arriving driver must be added at the so

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

### 13.3 The inside story

We now discuss some details regarding arrays and array accesses. This will specially be useful for understanding how we define functions for operating on arrays. To make the discussion more concrete, suppose we have the following definitions.

```
int p=5, q[5]={11,12,13,14,15}, r=9;
float s[10];
```

Say each variable of type int is most commonly given 4 bytes of memory, and so is a float. Thus we know the above definitions will cause 4 bytes of memory to be reserved for p, 4 × 5 = 20 bytes for q, 4 for r, and 4 × 10 = 40 bytes for s. We have also said that the memory given for an array is contiguous. Thus, the memory for q will start at a certain address, say Q, and go on to address Q + 19. The notion of addresses is as per our discussion in Chapter 2 and Section 9.8. Consistent with this description, Figure 13.3 shows how space might have been allocated for these variables.

Next we consider what happens when during execution we encounter a reference to an array element, e.g. q[expression]. How does the computer know where this element is stored? Of course, first the expression must be evaluated. Suppose its value is some v. Then we know that we want the element of q of index v. But because the elements are stored in order, we also know that the element with index v is stored at Q + 4v, where Q is the starting address for q. Thus if v = 3 then we would want q[3], which is stored from Q + 12. In general, the vth element of an array which is stored starting at address A would be at A + kv, where k is the number of bytes needed to store a single element.

So the important point is, that to get to an array element, the computer must evaluate the index expression, and even after the expression is evaluated it must perform the multiplication and addition to get the address A + kv. This is in contrast to how the computer gets the address for an ordinary variable such as p. In this case, the computer already knows where it stored p, and so it can get to it directly. Do note however that the extra work needed to figure out where the element is stored is independent of the length of the array.

### 13.3.1 Out of range array indices

Suppose now that our program has a statement q[5]=17;. Using the formula A + kv given above, the computer would try to store 17 in the int beginning at the address Q + 4 × 5 = Q + 20. Notice that this is outside the range of memory allocated for q. In fact, it is quite possible, as shown in our layout of Figure 13.3, that r is given the memory Q + 20 through Q + 23. Then the statement q[5]=17 might end up changing r! Likewise it is conceivable that a statement like q[-1]=30; might end up changing p.

Suppose on the other hand, we wrote q[10000]=18;. This would require us to access address Q + 40000. It is conceivable that there isnt any memory at this address. Many computers have some circuits to sense if an access is made to a non-existent address or even some forbidden addresses. The details of this are outside the scope of this book, but if this happens, then the program might halt with an error message. In any case, it is most important to ensure that array indices are within the required range.

### 13.3.2 The array name by itself

So far we have not said whether the name of an array can be used in the program by itself, i.e. without specifying the index. It turns out that C++ allows this.

In C++, the name of an array by itself is defined to have the value equal to the starting address from where the array is stored. This is an important place where arrays work differently from vectors, as we will see in Chapter 20.

Continuing our example of Figure 13.3, since the array q is stored starting at address Q,
