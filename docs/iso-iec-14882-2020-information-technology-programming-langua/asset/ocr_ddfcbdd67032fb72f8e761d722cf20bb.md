[Example 2:

```
namespace X {
    void p() {
        q();
        extern void q();
    }
    void middle() {
        q();
    }
    void q() { /* ... */ }
}
void q() { /* ... */ }
```

— end example]

8 Names not covered by these rules have no linkage. Moreover, except as noted, a name declared at block scope (6.4.3) has no linkage.

9 Two names that are the same (6.1) and that are declared in different scopes shall denote the same variable, function, type, template or namespace if

+   (9.1) — both names have external or module linkage and are declared in declarations attached to the same module, or else both names have internal linkage and are declared in the same translation unit; and
+   (9.2) — both names refer to members of the same namespace or to members, not by inheritance, of the same class; and
+   (9.3) — when both names denote functions or function templates, the signatures (3.45, 3.47) are the same.

If multiple declarations of the same name with external linkage would declare the same entity except that they are attached to different modules, the program is ill-formed; no diagnostic is required.

> [Note 2: using-declarations, typedef declarations, and alias-declarations do not declare entities, but merely introduce synonyms. Similarly, using-directives do not declare entities. Enumerators do not have linkage, but can serve as the name of an enumeration with linkage (9.7.1). — end note]

10 If a declaration would redeclare a reachable declaration attached to a different module, the program is ill-formed.

[Example 3:

```
"decls.h":
    int f();
    int g();
Module interface of M:
    module;
    #include "decls.h"
    export module M;
    export using ::f;
    int g();
    export int h();
    export int k();
Other translation unit:
    import M;
    static int h();
    int k();
```

— end example]

As a consequence of these rules, all declarations of an entity are attached to the same module; the entity is said to be attached to that module.

11 After all adjustments of types (during which typedefs (9.2.4) are replaced by their definitions), the types specified by all declarations referring to a given variable or function shall be identical, except that declarations