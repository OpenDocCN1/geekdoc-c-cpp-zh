

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

注意，我们添加了检查以查看当司机要进入时数组 driverID 是否已满，以及当顾客到达时其中是否至少有一个元素。

你可能会认为也许有一种方法可以编写程序，而不必在我们分配索引为 0 的司机时向上移动 driverID 中的条目。不是在数组中向上移动司机，我们能否不调整我们对队列前端位置的看法？确实这可行。但这需要更细致的注意。要正确地做到这一点，也许值得考虑我们如何在没有计算机的情况下调度出租车。

## 没有计算机的调度

思考任何问题，包括出租车调度，如何在没有计算机的情况下解决，这总是值得的。假设调度员在黑板上自上而下地写下司机 ID 号码，随着司机的报告。当司机到达时，我们在列表底部放下号码。当乘客进来时，列表顶部的号码交给乘客，然后该号码被擦除。

为了简单起见，假设我们的黑板只能容纳 100 个电话号码。管理黑板上的这个空间结果证明有点棘手。假设有 60 名司机报告，你从顶部开始写下他们的号码。假设接下来有 50 名乘客，所以你将他们与前 50 个号码匹配，然后擦除它们。此时你只有 10 个号码在板上，然而，它们不在板顶，而是在板中间开始。假设现在又有 60 名司机报告。你会将其中 40 个号码放在你板上已有的 10 个号码下方，这会带你到板底。剩下的 20 个应该放在哪里？自然是从顶部再次开始写号码，就好像板的底部与顶部相连一样。把黑板想象成形成圆柱体的曲面！因此此时，你有 70

![](img/c7233aedab7e4c7cad32a7615b6a4783_225_0.png)

板上的号码。它们从位置 50 开始（最上面的位置为 0），一直到最后一个位置 99。然后它们“环绕”，因此最后的 20 个号码占据位置 0 到 19。位置 20–49 然后未使用。这不应该使我们困惑；说我们在第一个等待司机旁边做一个标记。当我们分配司机时，我们从板上擦除号码，并将标记向下移动一位。这只要在任何时候等待的出租车司机数量不超过 100 就能很好地工作。

## 在计算机上模拟黑板

我们的程序将镜像上面给出的动作。我们在分配司机时不向上移动司机，而是有一个变量 `front`，它将始终包含包含最早等待未分配司机的 driverID 元素的索引。这执行了调度员在板上放置的标记的功能。

如果有 `nWaiting` 名司机在等待客户，他们的 ID 将出现在从 `front` 开始的位置。我们在说这件事时需要稍微小心：当板填满底部并且调度员被迫从顶部再次开始写号码时会发生什么？我们希望以某种方式说在最后一个索引 n−1（即板的“底部”）之后的“下一个”索引是索引 0（即板的“顶部”）。所以不是说 `front` 之后的下一个索引是 `front+1`，我们将说它是 `(front+1) % n`。如果 `front` 有某个值 `i<n−1`，那么 `(front+1) % n` 只是 `i+1`。然而，如果 `front` 等于 `n−1`，那么 `(front+1) % n` 确实会变成我们希望的 0。因此我们将简单地要求如果有 `nWaiting` 名司机在等待，他们的 ID 将位于索引 `front`、`(front + 1) % n`、…、`(front + nWaiting − 1) % n`。

接下来我们考虑司机到达时要执行的操作。如前所述，我们仅在 driverID 未满时才接受 ID。到达司机的 ID 必须添加到该位置

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

