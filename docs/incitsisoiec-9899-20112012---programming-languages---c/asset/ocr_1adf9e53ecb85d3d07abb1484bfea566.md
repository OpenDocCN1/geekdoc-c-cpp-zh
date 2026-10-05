# 3.19 value

precise meaning of the contents of an object when interpreted as having a specific value

# 3.19.1 implementation-defined value

unspecified value where each implementation documents how the choice is made

# 3.19.2 indeterminate value

either an unspecified value or a trap representation

# 3.19.3 unspecified value

valid value of the relevant type where this International Standard imposes no requirements on which value is chosen in any instance

NOTE An unspecified value cannot be a trap representation.

# 3.19.4 trap representation

an object representation that need not represent a value of the object type

# 3.19.5 perform a trap

interrupt execution of the program such that no further operations are performed

NOTE In this International Standard, when the word “trap” is not immediately followed by “representation”, this is the intended usage. 2)

# 3.20 [x]

ceiling of x: the greatest integer greater than or equal to x

EXAMPLE [2.4] is 3,[-2.4] is -2.

# 3.21 [x]

floor of x: the greatest integer less than or equal to x

EXAMPLE [2.4] is 2,[-2.4] is -3.

> 2) For example, “Trapping or stopping (if supported) is disabled...” (F.8.2). Note that fetching a trap might perform a trap but is not required to (see 6.2.6.1).