+   - An array’s elements can be initialized when the array is defined by following the definition with an equals sign and braces, `{}`, containing a comma-separated *list of initializers* (p. 248). If there are fewer initializers than array elements, the remaining elements are initialized to zero.
+   - The statement `int n[10] = {0};` explicitly initializes the first element to zero and initializes the remaining nine elements to zero because there are fewer initializers than array elements.
+   - If the array size is omitted from a definition with an initializer list, the compiler determines the array’s number of elements from the number of initializers.
+   - The `#define` preprocessor directive can define a **symbolic constant**—an identifier that the preprocessor replaces with replacement text before the program is compiled. When a program is preprocessed, all occurrences of the symbolic constant are replaced with the replacement text (p. 249). Using symbolic constants to specify array sizes makes programs easier to read and more **modifiable**.
+   - C has **no array bounds checking** to prevent a program from referring to an element that does not exist. Thus, an executing program can “walk off” the end of an array without warning. You should ensure that all array references remain within the bounds of the array.

# ## Section 6.5 Using Character Arrays to Store and Manipulate Strings

+   - A string literal such as `"hello"` is really an array of individual characters in C.
+   - A character array can be initialized using a **string literal**. In this case, the array’s size is determined by the compiler based on the string’s length.
+   - Every string contains a special **string-termination character** called the **null character** (p. 255). The character constant representing the null character is `'\0'`.
+   - A character array representing a string should always be defined large enough to hold the number of characters in the string and the terminating null character.
+   - Character arrays also can be initialized with individual character constants in an initializer list.
+   - Because a string is really an array of characters, we can access individual characters in a string directly using array subscript notation.
+   - You can input a string directly into a character array from the keyboard using `scanf` and the conversion specification `%s`. The character array’s name is passed to `scanf` without the preceding `&` used with non-array variables.
+   - Function `scanf` reads characters from the keyboard until the first whitespace character is encountered—it does not check the array size. Thus, `scanf` can write beyond the end of an array. For this reason, when reading a string into a `char` array with `scanf`, you should always use a field width that’s one less than the `char` array’s size (e.g., `"%19s"` for a 20-`char` array).
+   - A character array representing a string can be output with `printf` and the `%s` conversion specification. The characters of the string are printed until a terminating null character is encountered.

# ## Section 6.6 Static Local Arrays and Automatic Local Arrays

+   - We can apply `static` to a local array definition so the function does not create and initialize the array in each call and destroy it each time the function exits. This reduces program execution time, particularly for programs with frequently called functions that contain large arrays.
+   - Arrays that are `static` are automatically initialized once at program startup. If you do not explicitly initialize a `static` array, that array’s elements are initialized to zero by the compiler.