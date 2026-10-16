An alternative physical organization lets each logical module have its own header defining the facilities it provides. Each .cpp file then has a corresponding .h file specifying what it provides (its interface). Each .cpp file includes its own .h file and usually also other .h files that specify what it needs from other modules in order to implement the services advertised in the interface. This physical organization corresponds to the logical organization of a module. The interface for users is put into its .h file, the interface for implementers is put into a file suffixed _impl.h, and the module’s definitions of functions, variables, etc., are placed in .cpp files. In this way, the parser is represented by three files. The parser’s user interface is provided by parser.h:

```
// parser.h:
namespace Parser { // interface for users
double expr(bool get);
}
```

The shared environment for the functions expr(), prim(), and term(), implementing the parser is presented by parser_impl.h:

```
// parser_impl.h:
#include “parser.h” #include “error.h” #include “lexer.h”
using Error::error;
using namespace Lexer;
namespace Parser { // interface for implementers
double prim(bool get);
double term(bool get);
double expr(bool get);
}
```

The distinction between the user interface and the interface for implementers would be even clearer had we used a Parser_impl namespace (§14.3.3).

The user’s interface in header parser.h is #include d to give the compiler a chance to check consistency (§15.3.1).

The functions implementing the parser are stored in parser.cpp together with #include directives for the headers that the Parser functions need:

```
// parser.cpp:
#include “parser_impl.h” #include “table .h”
using Table::table;

double Parser::prim(bool get) {/*...*/}
double Parser::term(bool get) {/*...*/}
double Parser::expr(bool get) {/*...*/}
```

Graphically, the parser and the driver’s use of it look like this:
parser.h lexer.h error.h table .h
parser_impl.h