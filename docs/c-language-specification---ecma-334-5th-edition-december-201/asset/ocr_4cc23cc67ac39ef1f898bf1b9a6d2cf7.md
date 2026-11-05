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

embedded-statement:
  ...
  fixed-statement

fixed-statement:
  fixed ( pointer-type fixed-pointer-declarators ) embedded-statement

fixed-pointer-declarators:
  fixed-pointer-declarator
  fixed-pointer-declarators , fixed-pointer-declarator

fixed-pointer-declarator:
  identifier = fixed-pointer-initializer

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