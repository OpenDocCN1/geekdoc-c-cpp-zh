Sec. 15.2 Lower Bounds on Searching Lists

Here is our first attempt at proofing the theorem.

**Proof 1:** We will try a proof by contradiction. Assume an algorithm $A$ exists that requires only $n-1$ (or less) comparisons of $K$ with elements of **L**. Because there are $n$ elements of **L**, $A$ must have avoided comparing $K$ with **L[$i$]** for some value $i$. We can feed the algorithm input $K$ in position $i$. Such an input is legal in our model, so the algorithm is incorrect.

Is this correct? Unfortunately no. First of all, any given algorithm need not necessarily skip $K$ in position $i$ in its $n-1$ searches. For example, it is not necessary that all algorithms search the list from left to right. It is not even necessary that all algorithms compare the same $n-1$ positions through the time.

We can try to dress up the proof as follows: **Proof 2:** On any run of the algorithm, if $n-1$ elements are compared against $K$, then *some* element position (call it position $i$) is skipped. It is possible that $K$ is in position $i$ at that time, and will not be found. Therefore, $n$ comparisons are required.

Unfortunately, there is another error that needs to be fixed. It is not true that all algorithms for solving the problem work by comparing elements of **L** against $K$. An algorithm might make useful progress by comparing elements of **L** against each other. For example, if we compare two elements of **L**, then the greater and find that this element is less than $K$, we know that the other element is also less than $K$. It seems intuitively obvious that such comparisons would not actually lead to a faster algorithm, but how do we know for sure? We would need to generalize the proof to this approach.

We will now present a useful abstraction for expressing the state of knowledge for the value relationships among sets of objects. A **total order** defines relationships within a collection of objects such that for every pair of objects, one is greater than the other. A **partially ordered set** or **poset** is a set on which only a partial order is defined. That is for purpose here, the partial order is the state of our current knowledge about the objects, that zero or more of the order relations between pairs of elements are known. We can represent this knowledge by drawing directed acyclic graphs (DAGs) showing the known relationships, as illustrated by Figure 15.1.

**Proof 3:** Initially, we know nothing about the relative order of the elements in **L**, or their relationship to $K$. So initially, we view the $n$ elements in **L** as being in separate partial orders. Any comparison between two elements in **L** can affect the structure of the partial orders. This is somewhat similar to the UNION/FIND algorithm implemented using pointer trees, described in Section 6.2.

Now, every comparison between elements in **L** can at combine two of the partial orders together. Any comparison between $K$ and an element, say $A$, in **L** can at best eliminate the partial order that contains $A$. Thus, if we spend $m$ comparisons