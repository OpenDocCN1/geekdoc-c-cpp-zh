# # 1.2 Floating declarations

An external floating declaration is a data declaration with a type specifier of the flavor floating type:

+   floating-type = / short | double | long | float /

and declarations which are identifiers. For example,

```
```
static long float x;
float y;
```
```

makes x the name of a floating variable of long precision, visible only in the enclosing program file, and y an externally visible single-precision floating variable. They may participate in expressions much as integers do, but with slightly different meaning attached to the operators. The operators relevant to floating variables are described in [3.2].

# # 1.3 Pointer declarations

An external pointer declaration is a data declaration with any flavor of type specifier and a declaration of the form

```
*declarator
```

For example,

```
```
int *ptr_to_int;
struct item **ptr_to_item;
```
```

declares ptr_to_int as the name of a variable of type pointer to integer and ptr_to_item as a variable of type pointer to a struct item. The structured type struct item is a composite type whose definition presumably occurs elsewhere, but note that the content of the structure need not be known to declare a pointer to it.

Recalling the earlier definition of variable, the unique aspect of a pointer variable is that its class of admissible values ranges over the locations (machine addresses) of other values of the type to which the pointer variable is specified to point.

The use of these variables will be described subsequently in several chapters.