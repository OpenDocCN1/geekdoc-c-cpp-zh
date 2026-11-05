binary-operator-declarator:
type operator overloadable-binary-operator ( type identifier , type identifier )

+   overloadable-binary-operator:
+   +
+   -
+   *
+   /
+   %
+   &
+   |
+   ^
+   <<
+   right-shift
+   ==
+   !=
+   >
+   <
+   >=
+   <=

conversion-operator-declarator:
implicit operator type ( type identifier )
explicit operator type ( type identifier )

operator-body:
block
;

constructor-declaration:
attributes_opt constructor-modifiers_opt constructor-declarator constructor-body

constructor-modifiers:
constructor-modifier
constructor-modifiers constructor-modifier

+   constructor-modifier:
+   public
+   protected
+   internal
+   private
+   extern