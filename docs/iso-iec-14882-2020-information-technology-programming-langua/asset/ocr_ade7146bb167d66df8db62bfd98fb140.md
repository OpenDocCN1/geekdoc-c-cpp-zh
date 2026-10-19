# ISO/IEC 14882:2020(E)

(2.2) — a namespace-definition that contains an exported declaration, or

(2.3) — a declaration within a header unit (10.3) that introduces at least one name.

3 An exported declaration that is not a module-import-declaration shall declare at least one name. If the declaration is not within a header unit, it shall not declare a name with internal linkage.

4 [Example 1:

Source file "a.h":

```
export int x;
```

Translation unit #1:

```
module;
#include "a.h"        // error: declaration of x is not in the
                       // purview of a module interface unit

export module M;
export namespace {}        // error: does not introduce any names
export namespace {
    int a1;                // error: export of name with internal linkage
}
namespace {
    export int a2;         // error: export of name with internal linkage
}
export static int b;       // error: b explicitly declared static
export int f();           // OK
export namespace N { }    // OK
export using namespace N; // error: does not declare a name
```

— end example]

5 If the declaration is a using-declaration (9.9) and is not within a header unit, all entities to which all of the using-declarators ultimately refer (if any) shall have been introduced with a name having external linkage.

[Example 2:

Source file "b.h":

```
int f();
```

Importable header "c.h":

```
int g();
```

Translation unit #1:

```
export module X;
export int h();
```

Translation unit #2:

```
module;
#include "b.h"
export module M;
import "c.h";
import X;
export using ::f, ::g, ::h;   // OK
struct S;
export using ::S;            // error: S has module linkage
namespace N {
    export int h();
    static int h(int);        // #1
}
export using N::h;            // error: #1 has internal linkage
```

— end example]

[Note 1: These constraints do not apply to type names introduced by typedef declarations and alias-declarations.

[Example 3:

```
export module M;
struct S;
export using T = S;          // OK, exports name T denoting type S
```