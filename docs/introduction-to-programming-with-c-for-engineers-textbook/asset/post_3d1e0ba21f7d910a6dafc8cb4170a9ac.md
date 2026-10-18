
# Table 3.8 Summary of pointer syntax and operators.

| Operation | Syntax | Examples |
|---|---|---|
| Defining a pointer | `const object_type * pointer_identifier = & object;`<br>`const object_type * pointer_identifier { & object };` | `int x = 100;`<br>`int * ptr = & x; // create`<br>`// pointer ptr and set it to x`<br><br>`std::string s { "Fox" };`<br>`const string & r { s };`<br><br>`double d {}; // C++ init`<br>`double * d_ptr { nullptr }; // C++`<br>`d_ptr = & d;` |
| Address operator | `& object` | `* ptr = 112;`<br>`// assign 112 to x via ptr` |
| Dereferencing operator | `* pointer_identifier` | `cout << * d_ptr << s_ptr;`<br>`// print "FoxFox"` |

# ## Things to Remember

- Pointers are objects that allow for indirect access to other objects
- Pointer types are defined in relation to the type of object they point to. Syntactically, a pointer type is obtained by joining an object type with the * symbol
- Pointers are more than bare object addresses in memory space since they “know” the object type they point to. As a result, pointers can be incremented or decremented to point at the next object, not at the next memory location
- There is a special type void * that is not associated with a particular type and that can be used to express a system address to any object
- Like all objects, pointers should be initialized during creation. To express an empty pointer, a special nullptr value is assigned to a pointer
- For indirect access in C++, references should be considered rather than bare pointers (Section 3.11)

# ### 3.13 Statements

_Statements_ are language constructions that let us control code execution. The first statements to learn and understand are the conditional statement `if` and the loop statement `for`. In Section 2.5.2, we created expressions. An expression that ends with a semicolon becomes a statement. But unlike expressions, statements do not have a value. In addition, declarations are statements; blocks (groupings) of statements are also statements. To begin, we will investigate the role of braces in C++.

# ### 3.13.1 Blocks of Statements and Access to Variables – The Role of Braces

In C and C++, pairs of braces { } play an important role. Their two contexts are as follows:

- Grouping type definitions of a `class`, `struct`, `enum`, or `namespace` (in the first three cases, the closing `}` should be followed by a semicolon `;`). For example, let’s analyze the following C++ code:

```
namespace CppBook
{
    // Defines an RGB pixel with three byte values
    class RGB_Pixel
    {
    public:
    enum EColor
    {
    kRed, kGreen, kBlue
    }; // Semicolon after enum definition
    unsigned char GetRed( void ) const { return fData[ kRed ]; }
    // ...
    private:
    // An array with 3 byte values
    std::array< unsigned char, kBlue + 1 > fData;
    }; // Semicolon to close class definition
} // No ; when closing a namespace (namespace can be split in many places)
```

There are three pairs of braces in this code. The first pair, between lines [2–21], serves to encompass the CppBook namespace. There is no semicolon after [21] since namespaces can be split into separate parts. The second pair of braces, lines [5–19], defines a simplistic version of the RGB_Pixel class for RGB pixel representation. There is a semicolon after the closing brace on line [19]. Finally, on lines [9–11], we see the definition of the enum EColor type, belonging to the RGB_Pixel class, which is also closed with a semicolon. On the other hand, the braces on line [13] outline the body of a function – this is the second category, discussed in the next bullet.

EColor in the previous code is an example of the *unscoped enumerated type* (the newer scoped enums are discussed in Section 3.14.6). This old-style enum can be directly used to serve as an array bound or array index (IBM: “C++0x, scoped enums” https://www.ibm.com/developerworks/rational/library/scoped-enums/scoped-enums-pdf.pdf Accessed 2020). If not directly specified, the first constant, kRed in this case, is assigned the value 0, the second is assigned 1, and so on. Thus on line [18], the size of the fData array is set to kBlue + 1, whereas on line [13] a value of a red color is read simply as fData[kRed].

- Grouping statements of a *function* or a *statement* and defining a *local variable context*. To see this in action, let’s analyze the following function, which is used to compute Fibonacci numbers (also discussed in Section 3.14.4):

```
cpp
// Returns a vector with Fibonacci numbers up to max_val
vector< int > FibonacciNumbers( const int max_val )
{ // LOCAL STACK no. 0 CREATED for local objects (variables)

    vector< int > fibo_num_vec;   // local object, scope in the function

    int a = 0, b = 1; // two variables a and b created - scope only in the function

    while( a < max_val )
    { // LOCAL STACK no. 1 CREATED for local objects (variables)

        fibo_num_vec.push_back( a );

        int tmp = a; // a temporary to exchange a and b - scope only in the while

        a = b;       // a becomes "old" b
        b = tmp + b; // b becomes a sum of "old" a and b

    } // LOCAL STACK no. 1 DELETED - tmp is destroyed

    return fibo_num_vec;    // returned local object
} // LOCAL STACK no. 0 DELETED - a, b, max_val, fibo_num_vec dead after this line
```

The braces between lines [3–23] define the body of the FibonacciNumbers function. They group all the statements and expressions of this function and also define the scope for local variables. This means each variable (object) defined within the block delimited by the current level of braces is alive, visible, and accessible only in this block (unless it is declared static). After execution exits the block defined by the braces, *all local variables are destroyed and cannot be used* in any form! This is sometimes forgotten, which leads to nasty bugs (e.g. returning the address of

- In the scope of the `FibonacciNumbers` function, one object `fibo_num_vec` of type `vector< int >` is defined on line [5]. This is a local object that will be available inside the function. Hence, its *scope* is the body of the function, i.e. between lines [3–23]. It is also visible in this scope. The scope and visibility are the same for objects `a` and `b` defined on line [7].

The second pair of braces, between lines [10–19], defines a block of the `while` loop, presented in Section 3.13.2.2. On line [14], a `tmp` object (variable) of type `int` is defined, which is placed on the second local stack associated with the `while` context. However, unlike `a`, `b`, and `fibo_num_vec`, the scope of `tmp` is limited exclusively to the body of the `while` loop. In other words, `tmp` cannot be accessed before or after the `while` and its block. The `tmp` is used as an auxiliary variable to change the values of `a` and `b` on lines [16–17]. The latter, as well as `fibo_num_vec`, are also visible in the `while` block since it is embedded in the broader scope of the function body. Regarding *visibility*, the name `tmp` is visible only in the `while` scope, and it would hide all other `tmp` names if they were defined outside of the `while` loop.[^12]

After the `while` terminates on line [19], the second local stack is destroyed, which entails the destruction of the local `tmp` object. This behavior is desirable since it frees us from having to worry about explicitly deleting objects. Hence, such local objects are *automatic variables*. Other types of objects are discussed in Section 5.1. Last but not least, local stacks usually have limited capacity, so they should not be used to store very large objects (say, hundreds of megabytes or more).[^13] Instead, the heap and dynamic allocations should be used for large objects, as discussed in Section 5.2.

The two language constructions just discussed should not be confused. In this section, dealing with statements, we will primarily use the second context.

# 3.13.2  C++ Statements

In this section, we summarize all the statements in C++.[^14] Versions available in the C++11 standards are marked with color. Understanding the details of statement operations is a key factor in learning the language, as well as in writing correct code.

# 3.13.2.1  Conditional Statements

Conditional statements let us follow a path of execution based on the value of a given Boolean condition. In this group, we have the `if-else` and the `switch` statements, explained in Table 3.9. Starting from C++11, we have new versions of these with inherent initialization blocks, which are also highlighted.

[^12] As an interesting experiment, we can substitute `tmp` for `fibo_num_vec`. Then two variables named `fibo_num_vec`—one of type `vector< int >` and the second of type `int`—would coexist in the `while` scope. However, such code is obfuscated and by no means recommended.

[^13] Stack and heap sizes can be set in the linker settings.

[^14] With only a few exceptions, the same statements can be used in C. Details are provided in Appendix 9.2.
