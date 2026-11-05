```
class-body:
  { class-member-declarations_opt }

class-member-declarations:
  class-member-declaration
  class-member-declarations class-member-declaration

class-member-declaration:
  constant-declaration
  field-declaration
  method-declaration
  property-declaration
  event-declaration
  indexer-declaration
  operator-declaration
  constructor-declaration
  destructor-declaration
  static-constructor-declaration
  type-declaration

constant-declaration:
  attributes_opt constant-modifiers_opt const type constant-declarators ;

constant-modifiers:
  constant-modifier
  constant-modifiers constant-modifier

constant-modifier:
  new
  public
  protected
  internal
  private

constant-declarators:
  constant-declarator
  constant-declarators , constant-declarator

constant-declarator:
  identifier = constant-expression
```