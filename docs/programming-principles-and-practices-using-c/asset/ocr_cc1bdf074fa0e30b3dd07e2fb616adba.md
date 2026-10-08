Please note how we again and again avoid doing complicated work and instead find simpler solutions – often relying on library facilities. That’s the essence of programming: the continuing search for simplicity. Sometimes that’s – somewhat facetiously – expressed as “Good programmers are lazy.” In that sense (and only in that sense), we should be “lazy”; why write a lot of code if we can find a way of writing far less?

# # 6.9 Program structure

Sometimes, the proverb says, it’s hard to see the forest for the trees. Similarly, it is easy to lose sight of a program when looking at all its functions, classes, etc. So, let’s have a look at the program with its details omitted:

```
```c++
#include "std_lib_facilities.h"

class Token { /* ... */};
class Token_stream { /* ... */};

void Token_stream::putback(Token t) { /* ... */}
Token Token_stream::get() { /* ... */}

Token_stream ts;      // provides get() and putback()
double expression();  // declaration so that primary() can call expression()

double primary() { /* ... */}     // deal with numbers and parentheses
double term() { /* ... */}        // deal with * and /
double expression() { /* ... */}  // deal with + and –

int main() { /* ... */}   // main loop and deal with errors
```
```

The order of the declarations is important. You cannot use a name before it has been declared, so **ts** must be declared before **ts.get()** uses it, and **error()** must be declared before the parser functions because they all use it. There is an interesting loop in the call graph: **expression()** calls **term()** which calls **primary()** which calls **expression()**.