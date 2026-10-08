
16.7.4. Overload the * operator to perform matrix multiplication.

16.7.5. Let us define some terminology. \( L \) is a pseudo-square root of a matrix, \( A \), if \( A = LL^{T} \).

An \( n \times n \) matrix, \( A \), is said to be positive-definite if for all non-zero vectors \( v \), we have \( v^{T}Av > 0 \).

It turns out that all positive-definite symmetric matrices, \( A \), have a pseudo-square root. There is a unique lower-triangular pseudo-square root called the *Cholesky decomposition* of \( A \).

The Cholesky decomposition is useful for simulating multi-dimensional stochastic processes as described in Section 18.11. We will now describe how to compute the Cholesky decomposition mathematically. You should write the code to compute it numerically.

The matrix \( L \) can be computed using the equations:

\[
L_{i,j} = 
\begin{cases} 
\sqrt{A_{j,j} - \sum_{k=1}^{j-1} L_{j,k}^{2}} & i = j \\
\frac{1}{L_{j,j}} \left( A_{i,j} - \sum_{k=1}^{j-1} L_{i,k}L_{j,k} \right) & i < j \\
0 & i > j .
\end{cases}
\]

Although \( L \) appears on both sides of the equation, you should note that if you compute the terms of the matrix \( L \) row by row and then from left to right, you will find that each term required on the right-hand side of these equations has already been computed.

## 16.8 Summary

In terms of the C++ language, we have studied the following topics:

- const pointers.
- How to write two member functions: one that works on const instances; one that works on standard instances.
- How to overload operators such as \(+\), \(\ast\), and \(\geq\).
- How to overload the \(<<\) operator to make objects easy to print.
- How to overload \(+=\), \(-=\). Note the special rules about what parameters these take and returning *this. Most C++ operators can be overloaded. For each operator there are standard best practices on how it should be implemented, what the return type should be, and whether or not it should be written as a member function. Consult a text such as [13] for details.
- How to write a destructor for classes that manage memory and other resources. Note that most classes don't need a destructor.
- The rule of three: Whenever we write a destructor we write a copy constructor and override `=`.

Although we have implemented a sophisticated Matrix class in this chapter, we have done so purely to illustrate C++ techniques. Libraries containing much better Matrix implementations already exist.

### Tip: Go easy on pointers and operator overloading

- Using pointers and operator overloading is justified for a Matrix class because we'll use it so often.
- Pointers are only really justified in our implementation for educational purposes. The code we've written would perform as well if we had used `vector`. If we had done this we would not have needed to write a destructor, copy constructor, or assignment operator.
- Operator overloading is only justified because we come with expectations on how to add and multiply matrices. Don't overload operators to give them strange meanings. This just makes code hard to read.
- Realistically, a data structure such as a Matrix is the kind of class you should expect to find in a library rather than spending time writing it yourself.

## Chapter 17

### An Overview of Templates

We have already seen data types involving angle brackets, such as

```cpp
vector<double> v;
```

Code involving angle brackets is written using a C++ language feature called templates. In this chapter we will give a brief overview of how to write template functions and classes.

Templates are quite a difficult subject in practice. We have already said that you can think of C++ as consisting of three languages: C, an object-oriented language, and the language of templates. Learning a new language is a significant undertaking. For this reason we will only describe the basic ideas of template programming in this chapter. You should consult another reference such as [17] if you wish to write your own template library.

## 17.1 Template functions

Consider the following code to compute the maximum of a pair of numbers.

```cpp
inline double findMax( double x, double y ) {
    if (x<y) {
        return x;
    } else {
        return y;
    }
}

inline float findMax( float x, float y ) {
    if (x<y) {
        return x;
    } else {
        return y;
    }
}
```

This code violates the Once and Only Once principle because we have written essentially the same function twice, the only difference is that the types are different in the different function declarations.

Templates provide a solution to this problem. The following single template function allows us to find the maximum of either doubles or floats.

```cpp
template <typename T>
inline T findMax(T x, T y) {
    if (x < y) {
        return y;
    }
    else {
        return x;
    }
}
```

When you write a templated function, you don’t specify all the types of the parameters to your function. Instead, you provide a list of dummy variables, called template parameters, which can be replaced as necessary with the required types. In this example, we have one template parameter and it is called T.

In our example we specify that we are writing a template function and it has a template parameter called T, by writing:

```cpp
template <typename T>
```

The remaining code in our template function is then a copy of the desired code to compute the maximum but using the dummy variable T to represent the type.

We can then use our findMax function equally well with any type that provides an implementation of <. This includes float, double but also int and even string. This is tested using the following code:

```cpp
void testMax() {
    ASSERT(findMax(3, 1)==3); // ints
    ASSERT(findMax(2.0, 3.0) == 3.0); // doubles
    ASSERT(findMax(string("ant"),
    string("zoo")) == string("zoo"));
}
```

One unusual feature of templated functions is that the definition is normally put in the header file and not in a .cpp file. The actual rule is that any declaration and definition should be in the same file. So if you are writing a library function, the definition must be in the header file because that is where the declaration has to be.

The reason for this rule is that the code for a template function is not fully compiled until the template is actually used. It cannot be compiled until the template is used because the types are not yet known. This means that users of your library will need to have access to the code required to define all your templated functions. This in turn means that these definitions need to be in the header file.

### Danger!

If you are writing a templated library function, the definitions and declarations must be in the header files.

## 17.2 Template classes

The most visible use of template classes in C++ is in data types such as **vector<double>**. The syntax for template classes is very similar to that used for template functions.

Let us suppose we want to write a very simple data structure class called **SimpleVector**, which stores a vector of a fixed size **n** and allows the user to access the values at index **i** using functions **set** and **get**. We would also like to be able to use the same class to store values of any type.

To do this we write the class in the usual way, except we use a template parameter **T** as a placeholder for the type of data stored. Here is the code for our SimpleVector class.

```cpp
template <typename T>
class SimpleVector {
 public:
   /* Constructor */
   SimpleVector(int size);
   /* Destructor */
   ~SimpleVector() {
     delete[] data;
   }
   /* Access data */
   T get(int index) {
     return data[index];
   }
   /* Access data */
   void set(int index, T value) {
     data[index] = value;
   }
}
```
