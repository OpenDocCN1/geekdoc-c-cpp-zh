
interface-member-declarations:
  interface-member-declaration
  interface-member-declarations interface-member-declaration

interface-member-declaration:
  interface-method-declaration
  interface-property-declaration
  interface-event-declaration
  interface-indexer-declaration

interface-method-declaration:
  attributes_opt new_opt return-type identifier type-parameter-list
  ( formal-parameter-list_opt ) type-parameter-constraints-clauses_opt ;

interface-property-declaration:
  attributes_opt new_opt type identifier { interface-accessors }

interface-accessors:
  attributes_opt get ;
  attributes_opt set ;
  attributes_opt get ; attributes_opt set ;
  attributes_opt set ; attributes_opt get ;

interface-event-declaration:
  attributes_opt new_opt event type identifier ;

interface-indexer-declaration:
  attributes_opt new_opt type this [ formal-parameter-list ] { interface-accessors }

## B.2.11 Enums

```
enum-declaration:
  attributes_opt enum-modifiers_opt enum identifier enum-base_opt enum-body ;_opt

enum-base:
  : integral-type

enum-body:
  { enum-member-declarations_opt }
  { enum-member-declarations , }

enum-modifiers:
  enum-modifier
  enum-modifiers enum-modifier
```

## B.2.12 Delegates

## B.2.13 Attributes

```
enum-modifier:
  new
  public
  protected
  internal
  private

enum-member-declarations:
  enum-member-declaration
  enum-member-declarations , enum-member-declaration

enum-member-declaration:
  attributes_opt identifier
  attributes_opt identifier = constant-expression

delegate-declaration:
  attributes_opt delegate-modifiers_opt delegate return-type
  identifier variant-type-parameter-list
  ( formal-parameter-list_opt ) type-parameter-constraints-clauses_opt ;

delegate-modifiers:
  delegate-modifier
  delegate-modifiers delegate-modifier

delegate-modifier:
  new
  public
  protected
  internal
  private

global-attributes:
  global-attribute-sections

global-attribute-sections:
  global-attribute-section
  global-attribute-sections global-attribute-section

global-attribute-section:
  [ global-attribute-target-specifier attribute-list ]
  [ global-attribute-target-specifier attribute-list , ]
```

## B. Grammar

```
global-attribute-target-specifier:
    global-attribute-target :

global-attribute-target:
    assembly
    module

attributes:
    attribute-sections

attribute-sections:
    attribute-section
    attribute-sections attribute-section

attribute-section:
    [ attribute-target-specifier_opt attribute-list ]
    [ attribute-target-specifier_opt attribute-list , ]

attribute-target-specifier:
    attribute-target :

attribute-target:
    field
    event
    method
    param
    property
    return
    type

attribute-list:
    attribute
    attribute-list , attribute

attribute:
    attribute-name attribute-arguments_opt

attribute-name:
    type-name

attribute-arguments:
    ( positional-argument-list_opt )
    ( positional-argument-list , named-argument-list )
    ( named-argument-list )
```

```
positional-argument-list:
    positional-argument
    positional-argument-list  ,  positional-argument
```

```
positional-argument:
    argument-name<sub>opt</sub>  attribute-argument-expression
```

```
named-argument-list:
    named-argument
    named-argument-list  ,  named-argument
```

```
named-argument:
    identifier  =  attribute-argument-expression
```

```
attribute-argument-expression:
    expression
```

## B.3 Grammar Extensions for Unsafe Code

```
class-modifier:
    ...
    unsafe
```

```
struct-modifier:
    ...
    unsafe
```

```
interface-modifier:
    ...
    unsafe
```

```
delegate-modifier:
    ...
    unsafe
```

```
field-modifier:
    ...
    unsafe
```

```
method-modifier:
    ...
    unsafe
```

```
property-modifier:
  ...
  unsafe

event-modifier:
  ...
  unsafe

indexer-modifier:
  ...
  unsafe

operator-modifier:
  ...
  unsafe

constructor-modifier:
  ...
  unsafe

destructor-declaration:
  attributes_opt extern_opt unsafe_opt ~ identifier ( ) destructor-body
  attributes_opt unsafe_opt extern_opt ~ identifier ( ) destructor-body

static-constructor-modifiers:
  extern_opt unsafe_opt static
  unsafe_opt extern_opt static
  extern_opt static unsafe_opt
  unsafe_opt static extern_opt
  static extern_opt unsafe_opt
  static unsafe_opt extern_opt

embedded-statement:
  ...
  unsafe-statement
  fixed-statement

unsafe-statement:
  unsafe block

type:
  ...
  pointer-type
```

```
pointer-type:
    unmanaged-type *
    void *

unmanaged-type:
    type

primary-no-array-creation-expression:
    ...
    pointer-member-access
    pointer-element-access
    sizeof-expression

unary-expression:
    ...
    pointer-indirection-expression
    addressof-expression

pointer-indirection-expression:
    * unary-expression

pointer-member-access:
    primary-expression -> identifier type-argument-list_opt

pointer-element-access:
    primary-no-array-creation-expression [ expression ]

addressof-expression:
    & unary-expression

sizeof-expression:
    sizeof ( unmanaged-type )

fixed-statement:
    fixed ( pointer-type fixed-pointer-declarators ) embedded-statement

fixed-pointer-declarators:
    fixed-pointer-declarator
    fixed-pointer-declarators , fixed-pointer-declarator

fixed-pointer-declarator:
    identifier = fixed-pointer-initializer
```

fixed-pointer-initializer:
  & variable-reference
  expression

struct-member-declaration:
  ...
  fixed-size-buffer-declaration

fixed-size-buffer-declaration:
  attributes_opt fixed-size-buffer-modifiers_opt fixed buffer-element-type
  fixed-size-buffer-declarators ;

fixed-size-buffer-modifiers:
  fixed-size-buffer-modifier
  fixed-size-buffer-modifier fixed-size-buffer-modifiers

fixed-size-buffer-modifier:
  new
  public
  protected
  internal
  private
  unsafe

buffer-element-type:
  type

fixed-size-buffer-declarators:
  fixed-size-buffer-declarator
  fixed-size-buffer-declarator , fixed-size-buffer-declarators

fixed-size-buffer-declarator:
  identifier [ constant-expression ]

local-variable-initializer:
  ...
  stackalloc-initializer

stackalloc-initializer:
  stackalloc unmanaged-type [ expression ]

## C. References

IEEE. IEEE Standard for Binary Floating-Point Arithmetic. ANSI/IEEE Standard 754-1985. Available from http://www.ieee.org.

ISO/IEC. C++. ANSI/ISO/IEC 14882:1998.

Unicode Consortium. The Unicode Standard, Version 3.0. Addison-Wesley, Reading, Massachusetts, 2000, ISBN 0-201-616335-5.

This page intentionally left blank

## Index

A
\a escape sequence,81
Abstract accessors, 46, 557-558
Abstract classes
  and interfaces, 661
  overview, 468-469
Abstract events, 566
Abstract indexers, 567
Abstract methods, 35, 539-540
Access and accessibility
  array elements, 628
  containing types, 502-503
  events, 253
  indexers, 253, 300-301
  members, 23-24, 107, 496
  accessibility domains, 110-113
  constraints, 116-117
  declared accessibility, 107-109
  interface, 642-644
  pointer, 721-722
  in primary expressions, 283-288
  protected, 113-116
  nested types, 499-503
  pointer elements, 723
  primary expression elements, 298-301
  properties, 252, 555-556
Accessors
  abstract, 46, 557-558
  attribute, 695
  event, 564-565
  property, 43, 46, 547-853
Acquire semantics, 514
Acquisition in using statement, 445-446
add accessors
  attributes, 695
  events, 49, 564
Add method
  IEnumerable, 311
  List, 42
AddEventHandler method, 565
Addition operator
  described, 15
  uses, 337-340
Address-of operator, 724-725
Addresses
  fixed variables, 728-733
  pointers for, 714, 724-725
after state for enumerator objects, 593-596
Alert escape sequence,81
Aliases
  for namespaces and types, 456-461
  qualifiers, 464-466
  uniqueness, 466
Alignment enumeration, 58-59
Alloc method, 738
Allocation, stack, 736-738
AllowMultiple parameter,688

+   - Ambiguities
+     - grammar, 287–288
+     - in query expressions, 376
+   - Ampersands (&)
+     - for addresses, 716
+     - in assignment operators, 389
+     - definite assignment rules, 188–189
+     - for logical operators, 355–359
+     - for pointers, 724–725
+     - in preprocessing expressions, 87
+   - AND operators, 15
+   - Angle brackets (<>) for type arguments, 160
+   - Anonymous functions
+     - bodies, 367
+     - conversions, 219–221
+       - evaluation to delegate types, 165–166, 221–222
+       - evaluation to expression tree types, 222
+     - implementation example, 222–226
+     - implicit, 204
+     - definite assignment rules, 192
+     - delegate creation, 61
+     - dynamic binding, 369
+     - evaluation of, 373
+     - expressions, 165–166, 326, 364–366
+     - outer variables, 369–373
+     - overloaded, 368
+     - signatures, 365–366
+   - Anonymous objects, 317–319
+   - AppendFormat method, 31
+   - Applicable function members, 271–272
+   - Application domains, 99
+   - ApplicationException class, 681
+   - Applications, 4
+     - startup, 99–100
+     - termination, 100–101
+   - Apply method, 60
+   - Arguments, 28. See also Parameters
+     - command-line, 99
+     - for function members, 254–259
+       - type, 161–162
+       - type inference, 259–270
+   - Arithmetic operators, 331–332
+     - addition, 337–340
+     - division, 334–335
+   - multiplication, 332–333
+   - pointer, 725–726
+   - remainder, 336–337
+   - shift, 344
+   - subtraction, 340–342
+   - ArithmeticException class, 335, 685
+   - Arrays and array types, 625
+     - access to, 299–300, 628
+     - content, 13
+     - conversions, 200
+     - covariance, 200, 629–630
+     - creating, 628
+     - description, 8, 155
+     - elements, 53, 171, 628
+     - with foreach, 429
+     - IList interface, 627–628
+     - initializers, 55, 630–632
+     - members, 106, 628
+     - new operator for, 53, 55, 312–315
+     - overview, 53–55
+     - parameter, 31, 528–531
+     - and pointers, 719–720, 730–731
+     - rank specifiers, 625–626
+     - syntactic grammar, 804–805
+   - ArrayTypeMismatchException class
+     - description, 685
+     - type mismatch, 390–391, 629
+   - as operator, 353–355
+   - Assemblies, 4–5
+   - Assignment
+     - in classes vs. structs, 612
+     - definite. See Definite assignment
+     - fixed size buffers, 736
+   - Assignment operators, 16
+     - compound, 393–394
+     - event, 394–395
+     - overview, 389–390
+     - simple, 390–393
+   - Associativity of operators, 238–240
+   - Asterisks (*)
+     - assignment operators, 389
+     - comments, 69–70, 741–742
+     - multiplication, 332–333
+     - pointers, 713–716, 721
+     - transparent identifiers, 385
