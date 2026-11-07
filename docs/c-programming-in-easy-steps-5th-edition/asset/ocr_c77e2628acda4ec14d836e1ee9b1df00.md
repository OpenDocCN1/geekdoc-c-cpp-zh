# # Looping while

An alternative to the **for** loop, introduced above, uses the **while** keyword, followed by an expression to be evaluated. When the expression is **true**, statements contained within braces following the test expression will be executed. The expression will then be evaluated again, and the **while** loop will continue until the expression is found to be **false**.

The loop’s statement block **must** contain code that will affect the tested expression in order to change the evaluation result to **false**, otherwise an infinite loop is created that will lock the system! When the tested expression is found to be **false** upon its first evaluation, the **while** loop’s statement block will never be executed.

![](bbox=[0.118, 0.275, 0.207, 0.338])

If you accidentally start running an infinite loop, press the **Ctrl + C** keys to terminate the process.

A subtle variation of the **while** loop places the **do** keyword before the loop’s statement block and a **while** test after it, with this syntax:

```
do { statements-to-be-executed } while ( test-expression ) ;
```

In a **do-while** loop, the statement block will always be executed at least once -- because the expression is not evaluated until after the first iteration of the loop.

A **break** statement can be included in any kind of loop to immediately terminate the loop when a test condition is met. The **break** ensures no further iterations of that loop will be executed.

Similarly, a **continue** statement can be included in any kind of loop to immediately terminate that particular iteration of the loop when a test condition is met. The **continue** statement allows the loop to proceed to the next iteration.

![](bbox=[0.118, 0.559, 0.19, 0.603])

while.cpp

+   1. Start a new program by specifying the C++ library classes to include, and a namespace prefix to use

```
```cpp
#include <vector>              // Include vector support.
#include <iostream>
using namespace std ;
```
```

+   2. Add a main function containing a final **return** statement

```
```cpp
int main()
{
    // Program code goes here.
    return 0 ;
}
```
```

+   3. In the main function, insert statements to declare an integer vector and an integer variable loop counter

```
```cpp
vector <int> vec( 10 );
int i = 0 ;
```
```

+   4. Next, insert a **while** loop to assign a counter value to an element of the vector on each iteration

```
```cpp
while ( i < vec.size() )
{
    i++ ;                     // Increment the counter.
```
```