# 1.4 Array declarations

An external *array declaration* is a data declaration with any type specifier and a declaration of the form

`identifier [ constant-expr_opt ]`

The *constant-expr* must be a positive integer constant, calculable at compile-time, and defines the multiplicity N of the array. The valid subscripts range from 0 to N−1. For example,

`float point_3d[3];`

declares *point_3d* as an array variable consisting of three subvariables *point_3d[0]*, *point_3d[1]*, and *point_3d[2]* each of type *float*. The expressions *point_3d[2]*, *point_3d[1]*, and *point_3d[1]-2]* are *variable-name-exprs*, each of which refers to one of the three floating variables making up the composite floating array variable *point_3d*.

The *constant-expr* specifying array size may be omitted when an initializer is present and the size is implied by the number of values supplied. Initializers for arrays are discussed in [2.4]. It also is permissible to omit the size when declaring the existence of an array that is defined elsewhere, perhaps in another program file. It is possible to declare variables that are arrays of arrays, and so on, as in

`char page[50][80];`

which makes *page* the name of an array variable composed of 50 like variables of size 80 characters. Then *page[0][0]* and *page[49][79]* denote the northwest and southeast corners, respectively. When a declaration contains array of array, and so forth, only the first size specification may be omitted, for otherwise the contained arrays would not be objects of known size.

The character strings described in [0.4] are literal arrays of characters and behave like *char* array names, except when used as initializers of named *char* arrays. For example, the string "C-compiler" really acts like the secret declaration `"string1` where `"string1` has been predeclared by

`static char "string1"[] = "C-compiler";`