# Drill

Get the test of **binary_search** to run:

+   1.  Implement the input operator for **Test** from §26.3.2.2.
2.  Complete a file of tests for the sequences from §26.3:
    a.  {1 2 3 5 8 13 21}  // an “ordinary sequence”
    b.  {}
    c.  {1}
    d.  {1 2 3 4}  // even number of elements
    e.  {1 2 3 4 5}  // odd number of elements
    f.  {1 1 1 1 1 1 1 1}  // all elements equal
    g.  {0 1 1 1 1 1 1 1 1 1 1 1}  // different element at beginning
    h.  {0 0 0 0 0 0 0 0 0 0 0 0 0 1}  // different element at end
3.  Based on §26.3.1.3, complete a program that generates
    a.  A very large sequence (what would you consider very large, and why?)
    b.  Ten sequences with a random number of elements
    c.  Ten sequences with 0, 1, 2 . . . 9 random elements (but still ordered)
4.  Repeat these tests for sequences of strings, such as {Bohr Darwin Einstein Lavoisier Newton Turing} .

# Review

+   1.  Make a list of applications, each with a brief explanation of the worst thing that can happen if there is a bug; e.g., airplane control – crash: 231 people dead; $500M equipment loss.
2.  Why don’t we just prove our programs correct?
3.  What’s the difference between unit testing and system testing?
4.  What is regression testing and why is it important?
5.  What is the purpose of testing?
6.  Why doesn’t **binary_search** just check its requirements?
7.  If we can’t check for all possible errors, what kinds of errors do we primarily look for?
8.  Where are bugs most likely to occur in code manipulating a sequence of elements?
9.  Why is it a good idea to test for large values?
10. Why do we often represent tests as data rather than as code?
11. Why and when would we use lots of tests based on random values?