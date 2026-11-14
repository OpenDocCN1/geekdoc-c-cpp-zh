The syntax is specified as

```
register type variable-name
```

A register variable can only have local scope or be declared a function parameter; Registered global variables are not permitted. In addition, such variables are restricted to those types that can fit into a register on the microprocessor. Because they are in a physical hardware register, not in the larger RAM memory, one cannot take the address of a register variable.

The persistence of a register variable is the same as that for an auto variable. The best place to use them is in tight loops where access speed is important in minimizing the loop time and they are not going to change often. Access to a registered variable is limited to their scope.

# 6.4.3.6.5 TYPEDEF

The final storage class is the typedef, which is not actually a new storage class. The typedef qualifier permits the user to define synonyms for an existing type. It provides new data type names. It does not actually create a new type — it can only create a new name for an existing type. The new name acts like an alias for an existing data type. That data type can be either simple or complex.

The syntax is specified as

```
typedef type synonym
```

The typedef is in scope from the time of its definition. The notion of persistence is not applicable, and access to or utilization of a typedef variable is limited to the scope of the original variable. The typedef is similar to the preprocessor #define macro. The difference is that typedef’s are managed by the compiler (with appropriate type management) rather than the preprocessor, which merely substitutes text.

The following typedef allows us to define uint as a synonym for an unsigned int. Thereafter, the alias can be used as one would use any other type qualifier.

```
typedef unsigned int uint;
uint myVar = 0x56;
```

One should be careful when using typedefs. It is easy to redefine and thereby completely obfuscate and transmogrify the language. One should use the typedef to clarify code and make it more readable.

# 6.4.3.6.6 VOLATILE

Like the typedef, the keyword volatile is not a storage class; rather, it is a qualifier. Volatile is not something that one encounters in routine desktop applications. It is more likely to appear in embedded applications involving asynchronous internal or external tasks or specific