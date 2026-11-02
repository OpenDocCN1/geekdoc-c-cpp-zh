+   - The elements of an array can be initialized when the array is defined by following the definition with an equals sign and braces, { }, containing a comma-separated list of initializers (p. 250). If there are fewer initializers than elements in the array, the remaining elements are initialized to zero.

+   - The statement `int n[10] = {0};` explicitly initializes the first element to zero and initializes the remaining nine elements to zero because there are fewer initializers than there are elements in the array. It’s important to remember that automatic arrays are not automatically initialized to zero. You must at least initialize the first element to zero for the remaining elements to be automatically zeroed. This method of initializing the array elements to 0 is performed before program startup for *static* arrays and at runtime for automatic arrays.

+   - If the array size is omitted from a definition with an initializer list, the number of elements in the array will be the number of elements in the initializer list.

+   - The **#define** preprocessor directive can be used to define a symbolic constant—an identifier that the preprocessor replaces with replacement text before the program is compiled. When the program is preprocessed, all occurrences of the symbolic constant are replaced with the replacement text (p. 252). Using symbolic constants to specify array sizes makes programs more *modifiable*.

+   - C has no array bounds checking to prevent a program from referring to an element that does not exist. Thus, an executing program can “walk off” the end of an array without warning. You should ensure that all array references remain within the bounds of the array.

# *Section 6.5 Using Character Arrays to Store and Manipulate Strings*

+   - A string literal such as "hello" is really an array of individual characters in C.

+   - A character array can be initialized using a string literal. In this case, the size of the array is determined by the compiler based on the length of the string.

+   - Every string contains a special string-termination character called the null character (p. 258). The character constant representing the null character is `'\0'`.

+   - A character array representing a string should always be defined large enough to hold the number of characters in the string and the terminating null character.

+   - Character arrays also can be initialized with individual character constants in an initializer list.

+   - Because a string is really an array of characters, we can access individual characters in a string directly using array index notation.

+   - You can input a string directly into a character array from the keyboard using `scanf` and the conversion specifier `%s`. The name of the character array is passed to `scanf` without the preceding `&` used with non-array variables.

+   - Function `scanf` reads characters from the keyboard until the first white-space character is encountered—it does not check the array size. Thus, `scanf` can write beyond the end of the array.

+   - A character array representing a string can be output with `printf` and the `%s` conversion specifier. The characters of the string are printed until a terminating null character is encountered.

# *Section 6.6 Static Local Arrays and Automatic Local Arrays*

+   - A *static* local variable exists for the duration of the program but is visible only in the function body. We can apply *static* to a local array definition so that the array is not created and initialized each time the function is called and the array is not destroyed each time the function is exited in the program. This reduces program execution time, particularly for programs with frequently called functions that contain large arrays.

+   - Arrays that are *static* are automatically initialized once before program startup. If you do not explicitly initialize a *static* array, that array's elements are initialized to zero by the compiler.