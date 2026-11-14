
function-call operator. A class containing it is accordingly considered a static functor.

Click here to view code image

```
template <typename Target, typename Source, int N>
struct fsize_assign
{
    static void eval(Target& tar, const Source& src)
    {
        if constexpr (N > 0)
        fsize_assign<Target, Source, N-1>::eval(tar, src);
        tar[N] = src[N];
    }
};
```

To save ourselves from explicitly instantiating the argument types, we parameterize the eval instead of the class:

Click here to view code image

```
template <int N>
struct fsize_assign
{
    template <typename Target, typename Source>
    static void eval(Target& tar, const Source& src)
    {
        if constexpr (N > 0)
        fsize_assign<N-1>::eval(tar, src);
        tar[N] = src[N];
    }
};
```

Then the vector types can be deduced by the compiler when eval is called. Instead of a loop implementation, we call the recursive assignment functor in the operator:

Click here to view code image

```
template <typename T, int Size>
class fsize_vector
{
    static_assert(my_size > 0, "Vector must be larger than 0.");
    self& operator=(const self& that)
    {
        fsize_assign<my_size-1>::eval(*this, that);
        return *this;
    }

    template <typename Vector>
    self& operator=(const Vector& that)
    {
        fsize_assign<my_size-1>::eval(*this, that);
        return *this;
    }
};
```

The execution of the following code fragment:

Click here to view code image

```
fsize_vector<float, 4> v, w;
v[0] = v[1] = 1.0; v[2] = 2.0; v[3] = -3.0;
w = v;
```

shows the expected behavior (with the according print in `fsize_assign<>::eval`):

```
assign entry 0
assign entry 1
assign entry 2
assign entry 3
```

In this implementation, we replaced the loop with a recursion—counting on the compiler to `inline` the operations and the loop control. Otherwise the recursive function calls would be even slower than an ordinary loop.

This technique is only beneficial for small loops that run in L1 cache. Larger loops are dominated by loading the data from memory and the loop overhead is irrelevant. To the contrary, unrolling all operations with very large vectors usually decreases the performance because a lot of instructions need to be loaded, so the transfer of the data must wait. As mentioned before, compilers can unroll such operations by themselves and hopefully contain heuristics to decide when it is better not to. We have observed that the automatic unrolling of single loops is sometimes faster than explicit implementations like that above.

One would think that the implementation should be simpler with `constexpr` at least with the C++14 extensions. Unfortunately, this is not the case because we would mix compile-time arguments—the size—with run-time arguments—the vector references so that the `constexpr` function would be evaluated as an ordinary function. (We are working on an extension to overcome this limitation.)

## 5.4.2 Nested Unrolling

=> c++17/fsize_unroll_test.cpp

In our experience, most compilers unroll non-nested loops. Even good compilers that can handle certain nested loops will not be able to optimize every program kernel, in particular those with many template arguments that are instantiated with user-defined types. We will demonstrate here how to unroll nested loops at compile time with matrix vector multiplication as an example. To this end, we introduce a simplistic fixed-size matrix type:

Click here to view code image

```
template <typename T, int Rows, int Cols>
class fsize_matrix
{
    static_assert(Rows > 0, "Rows must be larger than 0.");
    static_assert(Cols > 0, "Cols must be larger than 0.");

    using self = fsize_matrix;
    public:
    using value_type = T;
    constexpr static int my_rows = Rows, my_cols = Cols;

    fsize_matrix(const self& that) { ... }

    // Cannot check column index here!
    T* operator[](int r) const { return data[r]; }
    T* operator[](int r) { return data[r]; }

    mat_vec_et<self, fsize_vector<T, Cols> >
    operator*(const fsize_vector<T, Cols>& v) const
    {
        return (*this, v);
    }

    private:
    T data[Rows][Cols];
};
```

The bracket operator returns a pointer for the sake of simplicity whereas a good implementation should return a proxy that allows for checking the column index (see §A.4.3.3). The multiplication with a vector is realized by returning the expression template mat_vec_et to avoid copying the result vector. Then the vector assignment is overloaded for our expression template type:

Click here to view code image

```
template <typename T, int Size>
class fsize_vector
{
    template <typename Matrix, typename Vector>
    self& operator=(const mat_vec_et<Matrix, Vector>& that)
    {
        using et = mat_vec_et<Matrix, Vector>;
        fsize_mat_vec_mult<et::my_rows-1, et::my_cols-1>::eval(
            that.A, that.v, *this);
        return *this;
    }
};
```

The static functor fsize_mat_vec_mult computes the matrix vector product and stores the result in the output vector:

Click here to view code image

```
template <int Row, int Col>
struct fsize_mat_vec_mult
{
    template <int R, int C> using mvm = fsize_mat_vec_mult<R, C>;

    template <typename Matrix, typename VecIn, typename VecOut>
    static void eval(const Matrix& A, const VecIn& v_in, VecOut& v_out)
    {
        if constexpr (Col == 0) {
            if constexpr (Row > 0) {
                mvm<Row-1, Matrix::my_cols-1>::eval(A, v_in, v_out);
            }
            v_out[Row] = A[Row][Col] * v_in[Col];
        } else {
            mvm<Row, Col-1>::eval(A, v_in, v_out);
            v_out[Row] += A[Row][Col] * v_in[Col];
        }
    }
};
```

The general case (in the `else` branch) increments an entry of `v_out` by the scalar product of `A[Row][Col]` and `v_in[Col]` after calling the operation for the preceding column. In column 0, we replace the increment by an ordinary assignment to initialize the result entry and switch to another row in the recursive call—except for row 0 where the recursion ends. Before C++17 we needed a master template and two specializations to realize the same behavior. With the inlining, our program will execute the operation `w = A * v` for vectors of size 4 as if we computed:

```
w[0] = A[0][0] * v[0];
w[0] += A[0][1] * v[1];
w[0] += A[0][2] * v[2];
w[0] += A[0][3] * v[3];
w[1] = A[1][0] * v[0];
w[1] += A[1][1] * v[1];
w[1] += A[1][2] * v[2];
...
```

Our tests have shown that such an implementation is really faster than the compiler optimization on loops.

### 5.4.2.1 Increasing Concurrency

A disadvantage of the preceding implementation is that all operations on an entry of the target vector are performed in one sweep. Therefore, the second operation must wait for the first one, the third for the second, and so on. The fifth operation can be done in parallel with the fourth, the ninth with the eighth, et cetera. However, this is a quite limited concurrency. We like having more parallelism in our program so that parallel pipelines in super-scalar processors or even SSEs (Streaming SIMD Extensions) and AVX (Advanced Vector Extensions) are enabled. Again, we can keep our fingers crossed and hope that the compiler will reorder the statements into our favorite order or take it in our own hands. More concurrency is provided when we traverse the result vector and the matrix rows in the “inner” loop:

```
w[0] = A[0][0] * v[0];
w[1] = A[1][0] * v[0];
w[2] = A[2][0] * v[0];
w[3] = A[3][0] * v[0];
w[0] += A[0][1] * v[1];
w[1] += A[1][1] * v[1];
...
```

We only need to restructure our `static` functor:

Click here to view code image

```
template <int Row, int Col>
struct fsize_mat_vec_mult_cm
{
    template <int R, int C> using mvm = fsize_mat_vec_mult_cm<R, C>;

    template <typename Matrix, typename VecIn, typename VecOut>
    static void eval(const Matrix& A, const VecIn& v, VecOut& w)
    {
        if constexpr (Col == 0) {
            if constexpr (Row > 0) {
                mvm<Row-1, 0>::eval(A, v, w);
                w[Row] = A[Row][0] * v[0];
            } else {
                if constexpr (Row > 0)
                mvm<Row-1, Col>::eval(A, v, w);
                else
                mvm<Matrix::my_rows-1, Col-1>::eval(A, v, w);
                w[Row] += A[Row][Col] * v[Col];
            }
        }
    };
};
```

In the general case, we decrement rows (instead of columns) in the recursive call, except for row 0 where we switch the column. Again, we have to initialize the according result entry in column 0 and also terminate the recursion. For comparison, the traditional implementation (before C++17) required a master template and three specializations.

Note that we perform the same operation on different data from which SIMD architectures can benefit. SIMD stands for Single Instruction, Multiple Data. Modern processors contain SSE units that perform arithmetic operations simultaneously on multiple floating-point numbers.
