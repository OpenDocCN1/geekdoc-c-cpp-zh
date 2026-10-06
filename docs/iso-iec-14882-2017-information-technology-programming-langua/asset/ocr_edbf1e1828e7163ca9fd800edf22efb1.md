# ISO/IEC 14882:2017(E)

```
S s3;
int i3 = {
    },\                 // Required initialization
    0,\                 // Required initialization
    0;                   // Initialization not required for A::s3 because A::i3 is also not initialized
}; // end example
```

11 When initializing a multi-dimensional array, the initializer-clause initializes the elements with the last (rightmost) index of the array varying the fastest (11.3.4). [Example:
int x[2] = { 3, 1, 4, 2 };
initializes x[0][0] to 3, x[0][1] to 1, x[1][0] to 4, and x[1][1] to 2. On the other hand,
float y[4] = {
{1}, {2}, {3}, {4}
initializes the first row of y (regarded as a two-dimensional array) and leaves the rest zero. — end example]

12 Braces can be eli-braced: if the initializer-list begins with a left brace, the subsequent comma-separated list of initializer-clauses initializes the elements of a subaggregate; it is erroneous for there to be more *initializer-clauses* than elements. If, however, for a subaggregate does not begin with a left brace, then only each *initializer-clause* from the list are used to initialize the first element of the subaggregate; any remaining *initializer-clauses* are left to initialize the next element of the aggregate of which the current subaggregate is an element. [Example:
float y[4][3] = {
{1, 3, 5},
{2, 4, 6},
{3, 5, 7};
is a completely-braced initialization: 1, 3, and 5 initializes the first row of y[0], namely y[0][0], y[0][1], and y[0][2]. Likewise the next two lines initialize y[1] and y[2]. The initializer ends early and therefore y[3] elements are initialized as explicitly initialized with an expression of the form *float()*, that is, initialized with 0.0. In the following example, braces in the initializer-list are el; however the initializer-list has the same effect as the completely-braced initializer-list of the above example,

```
float y[4][3] = {
1
```

initializer with a left brace, then the one for y[0] does not, three elements from the list are used. The next three are taken successively for y[1] and y[2]. — end example]

13 All implicit conversions (Clause 7) are considered when initializing the element with an *assignment-expression*. If the *assignment-expression* can initialize an element, the element is initialized. Otherwise, if the element is itself a subaggregate, brace elision is assumed and the *assignment-expression* is initialized. Otherwise, for the initialization of the first element of the subaggregate. [Note: As specified above, brace elision cannot apply to subaggregates with no elements; an *initializer-clause* for the entire subject is required. — end note |
Example:

```
struct A {
int i;
```

§ 11.6.1

©ISO/IEC 2017 - All rights reserved

227