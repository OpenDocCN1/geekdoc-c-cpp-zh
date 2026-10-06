# ISO/IEC 14882:2017(E)

```
enum-base:
  : type-specifier-seq
  enumerator-list:
    enumerator-definition
    enumerator-list , enumerator-definition
  enumerator-definition:
    enumerator
    enumerator = constant-expression
enumerator:
  identifier attribute-specifier-seq_opt
namespace-name:
  identifier
  namespace-alias
namespace-definition:
  named-namespace-definition
  unnamed-namespace-definition
  nested-namespace-definition
named-namespace-definition:
  inline_opt namespace attribute-specifier-seq_opt identifier { }
unnamed-namespace-definition:
  inline_opt namespace attribute-specifier-seq_opt { namespace-body }
nested-namespace-definition:
  namespace enclosing-namespace-specifier :: { namespace-body }
enclosing-namespace-specifier:
  identifier
  enclosing-namespace-specifier :: identifier
namespace-body:
  declaration-seq_opt
namespace-alias:
  identifier
namespace-alias-definition:
  namespace-specifier = qualified-namespace-specifier;
qualified-namespace-specifier:
  nested-name-specifier_opt namespace-name
using-declaration:
  using using-declarator-list;
using-declarator-list:
  using-declarator ..._opt
  using-declarator-list , using-declarator ..._opt
using-declarator:
  typename_opt nested-name unqualified-id
using-directive:
  attribute-specifier-seq_opt using namespace nested-name-specifier_opt namespace-name;
asm-definition:
  attribute-specifier-seq_opt asm { string-literal };
linkage-specification:
  extern string-literal { declaration-seq_opt }
  extern string-literal declaration
```

§ A.6
ISO/IEC 2017 - All rights reserved
1421