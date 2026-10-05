(6.7.2.1) specifier-qualifier-list:
type-specifier specifier-qualifier-list_opt
type-qualifier specifier-qualifier-list_opt

(6.7.2.1) struct-declarator:
struct-declarator
struct-declarator-list , struct-declarator

(6.7.2.1) struct-declarator:
declarator
declarator_opt : constant-expression

(6.7.2.2) enum-specifier:
enum identifier_opt { enumerator_list }
enum identifier_opt { enumerator_list , }
enum identifier

(6.7.2.2) enumerator-list:
enumerator
enumerator-list , enumerator

(6.7.2.2) enumerator:
enumeration-constant
enumeration-constant = constant-expression

(6.7.2.4) atomic-type-specifier:
_Atomic ( type-name )

(6.7.3) type-qualifier:
const
restrict
volatile
_Atomic

(6.7.4) function-specifier:
inline
_Noreturn

(6.7.5) alignment-specifier:
_Alignas ( type-name )
_Alignas ( constant-expression )

(6.7.6) declarator:
pointer_opt direct-declarator