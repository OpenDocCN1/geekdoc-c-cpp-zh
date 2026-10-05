# 19.2. EXCEPTION EXAMPLES

better illustrates the program's execution.

# Program Execution Timeline

![](bbox=[0.237, 0.219, 0.762, 0.417])

Figure 19.2: Function call interrupted by an exception. Neither the vectorint::at method, the find function, nor the process function completes its work and returns as usual to its caller. Control passes back to the catch block in the call chain.

Listing 19.3 (callexception.cpp) demonstrates that exceptions have the potential to radically alter the normal call and return pathways. In one sense an exception works like a “super goto” statement. The program's execution jumps to a previous point in its execution sequence, bypassing all functions in the call chain. Recall Section 6.3.2 discouraged the use of the goto statement except for to exit from a nested loop. This is the code in which goto instead of a super structured branching and looping constructs such as if/else, switch, while, and for to be difficult to extend and maintain. C++'s exception mechanism is different than a “super goto” in several important ways:

+   - A goto statement cannot jump to outside the code of the function in which it appears. Exceptions have no such limitation.
- The programmer must specify a destination (label) for a goto statement. the vector<int>::at method throws the exception. We can call at many different functions within a single program and use at in many different programs. The code within the method cannot possibly know where to go if it encounters an exceptional situation. An exception simply redirects the program's execution to the most recent try/catch block in the call chain that can handle the exception.

Listing 19.4 (strboundexcept.cpp) follows.

| Listing 19.4: strboundexcept.cpp |
| #include <iostream> |

©2014 Richard L. Halterman Draft date: January 26, 2014