easily visible to the client engineer. The danger of making them at file scope is less than that of making a using-directive at file scope, but risks still remain.

The fourth is for making using-directives. These are of very limited use: perhaps you are writing a slide for a presentation and you want to signal to the audience that you are using a particular namespace in some example code. For example:

Click here to view code image

```
#include <iostream>
using namespace std;

int main() {
    cout << "Hello, world!";
    return 0;
}
```

Rather than type std::cout, you are relying on the introduction of all symbols from the std namespace so far declared in the <iostream> header. It is very convenient.

Very, very convenient.

This is a very simple use of a using-directive, suitable for trivial code. In more complicated code surprising things happen, because a using-directive does not only introduce the new symbols into the current scope.

We’ll just say that again: a using-directive does not only introduce new symbols into the current scope. It does something rather more surprising, and we need to cover a little graph theory to work out what’s going on.

# Where do the symbols go?

First, we need to look at the idea of a directed acyclic graph, or DAG, a term coined by Bjarne Stroustrup’s office mate, Al Aho. A graph is a set of nodes with relation-ships between them. A directed graph is a set of nodes with relationships between them that only operate in one direction. For