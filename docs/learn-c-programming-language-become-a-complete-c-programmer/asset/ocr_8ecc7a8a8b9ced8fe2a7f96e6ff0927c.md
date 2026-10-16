(because namespaces are open; §14.2.5) we don’t have to. The lack of separate names need not lead to confusion because the physical layout of the program (see §15.3.2) naturally provides separate (file) names. Had we decided to use a separate implementation namespace, the design would not have looked different to users:

# Section 14.3.3 Interfaces and Implementations 405

```
namespace Parser { // user interface double expr(bool);
}

namespace Parser_impl { using namespace Parser;
// implementer interface

double prim(bool); double term(bool); double expr(bool);
using namespace Lexer; // use all facilities offered by Lexer using Error::error;
using Table::table;
}
```

or graphically:
Parser (user interface)
Parser_impl (implementer interface)
Driver code Parser code
For larger programs, I lean toward introducing _impl interfaces.

The interface offered to implementers is larger than the interface offered to users. Had this interface been for a realistically sized module in a real system, it would change more often than the interface seen by users. It is important that the users of a module (in this case, Driver using Parser) be insulated from such changes.

# 14.4 Composition Using Namespaces

In larger programs, we tend to use many namespaces. This section examines technical aspects of composing code out of namespaces.

# 14.4.1 Convenience vs. Safety

A using-declaration adds a name to a local scope. A using-directive does not; it simply renders names accessible in the scope in which they were declared. For example:

```
namespace X {
int i, j, k;
int k;

void f1() {
int i = 0;
using namespace X; // makenames from X accessible i++; // local i
j++; // X::j
k++; // error :X’skorthe global k? ::k++; // the global k
```