6 A declaration of a name with internal linkage is permitted within a header unit despite all declarations being implicitly exported (10.2).

> [Note 5: A definition that appears in multiple translation units cannot in general refer to such names (6.3). — end note]

A header unit shall not contain a definition of a non-inline function or variable whose name has external linkage.

7 When a module-import-declaration imports a translation unit T, it also imports all translation units imported by exported module-import-declarations in T; such translation units are said to be exported by T. Additionally, when a module-import-declaration in a module unit of some module M imports another module unit U of M, it also imports all translation units imported by non-exported module-import-declarations in the module unit purview of U.102 These rules can in turn lead to the importation of yet more translation units.

8 A module implementation unit shall not be exported.

> [Example 1:

Translation unit #1:

```
module M:Part;
```

Translation unit #2:

```
export module M;
export import :Part;    // error: exported partition :Part is an implementation unit
```

> — end example]

9 A module implementation unit of a module M that is not a module partition shall not contain a module-import-declaration nominating M.

> [Example 2:

```
module M;
import M;            // error: cannot import M in its own unit
```

> — end example]

10 A translation unit has an interface dependency on a translation unit U if it contains a declaration (possibly a module-declaration) that imports U or if it has an interface dependency on a translation unit that has an interface dependency on U. A translation unit shall not have an interface dependency on itself.

> [Example 3:

Interface unit of M1:

```
export module M1;
import M2;
```

Interface unit of M2:

```
export module M2;
import M3;
```

Interface unit of M3:

```
export module M3;
import M1;            // error: cyclic interface dependency M3 → M1 → M2 → M3
```

> — end example]

# 10.4 Global module fragment [module.global.frag]

global-module-fragment:
    module-keyword ; declaration-seqopt

> 1 [Note 1: Prior to phase 4 of translation, only preprocessing directives can appear in the declaration-seq (15.1). — end note]

2 A global-module-fragment specifies the contents of the global module fragment for a module unit. The global module fragment can be used to provide declarations that are attached to the global module and usable within the module unit.