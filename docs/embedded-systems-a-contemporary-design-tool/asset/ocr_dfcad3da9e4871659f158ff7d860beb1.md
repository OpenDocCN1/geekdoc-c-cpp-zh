![](bbox=[0.28, 0.08, 0.82, 0.42])

Figure 19.1 A Simple Combinational Logic Array

For the configuration above, with two input variables, call them A and B, we have four possible minterms:

A̅B̅, A̅B, AB̅, AB

and with the specified three outputs, we can express up to three different sums of product logic expressions based on which connections we choose to make (or break). In some implementations, all of the connections are present (in others, they are absent). To implement a logic equation, we simply remove (or make) some of the connections.

# EXAMPLE 19.1

Using the above device, we can implement the logical equation:

F = AB̅ + A̅B

+   First AND
+   Make the A and B̅ connections – these are indicated by small circles.
+   Second AND
+   Make the A̅ and B connections – these are indicated by small circles.
+   First OR
+   Make connections to the first two legs and no connection to the third leg.

We can see that we have an AND array and an OR array as the final implementation in Figure 19.2.

Utilizing such an architecture, we can realize any sum of products expression. The only restriction we have is the size of the device, that is, the number of input and output pins and the number of product terms available.