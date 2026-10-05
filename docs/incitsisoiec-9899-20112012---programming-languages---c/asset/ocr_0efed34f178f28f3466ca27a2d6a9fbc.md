NOTE 1 Two threads of execution update and access separate memory locations without interfering with each other.

NOTE 2 A bit-field and an adjacent non-bit-field member are in separate memory locations. The same applies to bit-fields, if one is declared inside a nested structure declaration and the other is not, or if they are separated by a zero-length bit-field declaration, or if they are separated by a non-bit-field member declaration. It is not safe to concurrently update two non-atomic bit-fields in the same structure if all members declared between them are (non-zero-length) bit-fields, no matter what the sizes of the intervening bit-fields happen to be.

EXAMPLE A structure declared as

```
struct {
    char a;
    int b:5, c:11, :0, d:8;
    struct { int ee:8; } e;
}
```

contains four separate memory locations: The member a, and bit-fields d and e.ee are each separate memory locations, and can be modified concurrently without interfering with each other. The bit-fields b and c constitute the fourth memory location. The bit-fields b and c cannot be concurrently modified, but b and a, for example, can be.

# 3.15

object region of data storage in the execution environment, the contents of which can represent values

NOTE When referenced, an object may be interpreted as having a particular type; see 6.3.2.1.

# 3.16

parameter

formal parameter formal argument (deprecated) object declared as part of a function declaration or definition that acquires a value on the entry to the function, or an identifier from the comma-separated list bounded by the parentheses immediately following the macro name in a function-like macro definition

# 3.17

recommended practice specification that is strongly recommended as being in keeping with the intent of the standard, but that may be impractical for some implementations

# 3.18

runtime-constraint

requirement on a program when calling a library function

NOTE 1 Despite the similar terms, a runtime-constraint is not a kind of constraint as defined by 3.8, and not needed be demonstrated at translation time.

NOTE 2 Implementations that support the extensions in annex K are required to verify that the runtime constraints for a library function are violated by the program; see K.3.1.4.