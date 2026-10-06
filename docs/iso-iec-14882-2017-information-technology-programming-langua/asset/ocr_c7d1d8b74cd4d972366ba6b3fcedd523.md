# ISO/IEC 14882:2017(E)

```
defining-type-specifier-seq
defining-type-specifier attribute-specifier-seq_opt
defining-type-specifier defining-type-specifier-seq
simple-type-specifier:
nested-name-specifier_opt type-name
nested-name-specifier template simple-template-id
nested-name-specifier_opt template-name
char
16_t
char32_t
wchar_t
bool
short
int
long
signed
unsigned
float
double
void
auto
decltype-specifier
type-name:
class-name
enum
typef-name
simple-template-id
decltype-specifier:
decltype ( expression )
decltype ( auto )
elaborated-id-type-specifier:
class-key attribute-specifier-seq_opt nested-name-specifier_opt identifier
class-key nested-name-specifier_opt simple-template-id
enum nested-name-specifier_opt identifier
enum-name:
identifier
enum-specifier:
enum-head { enumerator-list_opt }
enum-head ( enumerator-list , )
enum-head:
enum-key attribute-specifier-seq_opt enum-head-name_opt enum-base_opt
enum-head-name:
nested-name-specifier_opt identifier
opaque-enum-declaration:
enum-key attribute-specifier-seq_opt nested-name-specifier_opt identifier enum-base_opt ;\nenum-key:
enum
enum class
enum struct
```

§ A.6 ©ISO/IEC 2017 – All rights reserved 1420