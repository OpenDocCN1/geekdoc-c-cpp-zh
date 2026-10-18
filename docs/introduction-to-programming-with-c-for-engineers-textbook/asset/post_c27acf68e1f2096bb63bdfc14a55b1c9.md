
possible to “call” an object? The answer is that this is a function. What is called is a constructor of `fData`. Since it is of class `std::vector`, this constructor expects as its first argument the number of elements, and the second parameter is an initial value for these elements (see Table 3.4). In this case, the number of elements is the number of rows. However, the initial value is an example row – therefore, the object `RealVec( cols, initVal )` is provided as an initial value as a kind of a prototype. After that, on lines [14–18], the body of the `EMatrix` constructor-function follows. It is almost empty, though the only two lines [16–17] are occupied by calls to `assert` functions. As we already know, these are special use-functions that are usually active only in the *debug* version of software. Their role is to check the correctness of constructions or, as in this case, of passed parameters. In our `EMatrix` constructor, we require both dimensions to be larger than 0. This is to verify whether the passed dimensions of a matrix are greater than 0, since, although possible, a matrix of size 0 is not well-defined. However, if someone mistakenly tries to create `EMatrix` by providing 0 as its dimension, the program is stopped, a message is shown, and we can check the reason in the debugger window. This is a good way to control the behavior of our code in the testing stage.

Certainly, the requirement that the dimensions of a matrix be greater than 0 can be relaxed. As already mentioned, this is a mathematical, rather than a programming, constraint. For example, by adding default parameters to the `EMatrix` constructor, as follows

```
EMatrix( Dim rows = 0, Dim cols = 0, DataType initVal = 0.0 )
```

a constructor is obtained that can be called without providing any arguments – this is a *default constructor*. And as mentioned in Section 3.9, if data can be initialized with only `{}`, a constructor can be omitted. We will see many examples in future sections.

Moreover, the requirement to always pass dimensions during object construction has a consequence – an object does not have a default means of construction (i.e. without any additional parameters). In other words, explicitly defining the parametric constructor suppresses the automatic generation of a default constructor by the compiler. The lack of a default constructor imposes limitations on an object, as we will discuss.

Another design question is whether to allow or disallow changes to a matrix’s dimensions after it has been created. We have to make such design decisions quite often. They should be thoroughly analyzed, taking the consequences into consideration; and, even more important, they should be well commented in the code.

Returning to the definition of `EMatrix`, notice that there are two more member functions – `GetCols` on line [22] and `GetRows` on line [23] – that return the number of columns and rows in `EMatrix`. The operation of these functions should be clear by now, since in previous sections we discussed how to access the dimensions of a `RealMatrix`. However, two things that deserve explanation. First is the return type, which here is defined with `auto`. We could use `Dim`, but using `auto` is more versatile, as we will show many times. Second is the keyword `const`. Declaring functions `const` means the function has no intention of changing any member data (state).

Since `EMatrix` contains `fData` and extends its functionality, this construction is an object *wrapper* or an *adapter* design pattern (Gamma et al. 1994). We will see this ubiquitous and useful construction in many examples in this book (Section 4.8.4).

## Things to Remember

- Data member initialization in a `struct` (class) can be performed with a constructor that belongs to the group of *special member functions*
- A constructor that can be called without any argument is called a *default constructor*
- A constructor that takes arguments is called a *parametric constructor*
- Initialization of the data members in a constructor should be performed in the *constructor initialization list*, i.e. after the colon `:` and before the constructor body
- Data members are always initialized in the order in which they are declared in the class definition, so they also should be written in that order in the constructor initialization list
- Adding a parametric constructor to a struct (class) will suppress the automatic generation of the default constructor by the compiler (and other special members)

### 3.15.1  **EMatrix in an Object-Oriented Environment**

EMatrix was defined with the help of `struct`, which implies that all of its data and member functions are widely accessible and can be freely called from any EMatrix object.

```cpp
struct EMatrix
{

    RealMatrix fData; // data structure
}
```

The equivalent with the `class` keyword is as follows:

```cpp
class EMatrix
{
    public:
        RealMatrix fData; // data structure
}
```

Since `class` assumes all members to be private, adding the `public` keyword makes all data members and function members wide open, as is the case with `struct`. But obtaining the same functionality, just with different keywords, is not interesting. What is interesting is using OOP paradigms in our designs. The current version of `EMatrix` is close to being in the OO domain. To enter that domain, though, we at least need to make data private and add member functions. In Section 4.7, we will practice re-making `EMatrix` in the OO domain. Such changes to enhance the code’s features and quality are called *code refactoring* (Fowler 1999).

### 3.15.2  **Basic Operations with EMatrix**

Having defined `EMatrix`, let’s do some matrix computations, as shown in Listing 3.20. On lines [12–19], we print instructions to the user. On line [22], an object `matrix_1` with dimensions 3 × 4 is created. This involves the EMatrix constructor, which we discussed in the previous section. As a result, we can be sure that all matrix elements are set to zero.

Instead of writing all the computation steps in one big function, it is almost always better to organize the code into a number of specialized functions. Therefore, to enter and print matrix data, we use the `AskUserForMatrixData` and `ShowMatrix` functions. Similarly, `MultMatrix` performs matrix multiplication. To call them, we only need to provide their declarations, such as the ones on lines [4–6]. This way, we can use them now and postpone their full definitions until later in the code.

**Listing 3.20 Definition of the Easy_Matrix_Second_Test function with examples of using EMatrix to define, initialize, and multiply matrices (in EasyMatrix, EMTest.cpp).**

```cpp
// To use a function we only need to provide its declaration.
// However, to make a full program, function definitions must
// be added in some of the source files.
void AskUserForMatrixData( EMatrix & m );
void ShowMatrix( const EMatrix & m );
EMatrix MultMatrix( const EMatrix & a, const EMatrix & b );

// Here we show how to use EMatrix
void Easy_Matrix_Second_Test( void )
{
    std::cout << "------------------------------------------" << std::endl;
    std::cout << "In this example we will:" << std::endl;
    std::cout << "* Create a 3x4 matrix M1 (you will enter its data)" << std::endl;
    std::cout << "* Print M1" << std::endl;
    std::cout << "* Create a 4x2 matrix M2 (you will enter its data)" << std::endl;
    std::cout << "* Print M2" << std::endl;
    std::cout << "* Compute and print a product M1 * M2" << std::endl;
    std::cout << "------------------------------------------" << std::endl;

    EMatrix matrix_1( 3, 4 );
    AskUserForMatrixData( matrix_1 );
    std::cout << "You've just entered M1 - is it correct?" << std::endl;
    ShowMatrix( matrix_1 );

    EMatrix matrix_2( 4, 2 );
    AskUserForMatrixData( matrix_2 );
    std::cout << "You've just entered M2 - is it correct?" << std::endl;
    ShowMatrix( matrix_2 );

    std::cout << "The matrix product of M1 * M2 is:" << std::endl;
    ShowMatrix( MultMatrix( matrix_1, matrix_2 ) );
}
```

On line [23], the AskUserForMatrixData function is called to let the user enter values for the elements of matrix_1 from the keyboard. To verify its contents, matrix_1 is printed out on the screen by the ShowMatrix function, invoked on line [26]. Similarly, on lines [29-33], the matrix_2, this time with dimensions 4×2, is acquired and shown. Finally, the product of the two matrices is computed and immediately shown on line [37] by successive calls to the MultMatrix and ShowMatrix functions. More precisely, MultMatrix returns a temporary EMatrix object that is taken by ShowMatrix as its argument, which is then shown. As we know from matrix algebra, their product is a 3×2 matrix. We will return to the details of these computations shortly.

Note that of these functions, only AskUserForMatrixData changes the matrix passed to it. For this purpose, its argument is declared as a reference to an EMatrix object: that is, as EMatrix &. The other two functions only read values from their passed EMatrix arguments. Therefore, these are declared as constant references: const EMatrix &. This way, the passed objects are safe
