
## A.1 More Good and Bad Scientific Software

```cpp
sum+= vp[i] * wp[i];
return sum;
}

int cg(int size, double *x, double *b,
     void (*prec)(int, double*, double*), double eps)
{
    int i, j, iter= 0;
    double rho, rho_0, alpha;
    double *p= new double[size];
    double *q= new double[size];
    double *r= new double[size];
    double *z= new double[size];

    // r = A*x;
    r[0] = 2.0 * x[0] - x[1];
    for (int i= 1; i < size-1; i++)
        r[i] = 2.0 * x[i] - x[i-1] - x[i+1];
    r[size-1] = 2.0 * x[size-1] - x[size-2];

    // r = b-A*x;
    for (i= 0; i < size; i++)
        r[i]= b[i] - r[i];

    while (one_norm(size, r) >= eps) {
        prec(size, r, z);
        rho_0= dot(size, r, z);
        if (iter)
            for (i= 0; i < size; i++)
                p[i]= z[i];
    } else {
        for (i= 0; i < size; i++)
            p[i]= z[i] + rho / rho_1 * p[i];
    }

    // q = A * p;
    q[0] = 2.0 * p[0] - p[1];
    for (int i= 1; i < size-1; i++)
        q[i] = 2.0 * p[i] - p[i-1] - p[i+1];
    q[size-1] = 2.0 * p[size-1] - p[size-2];

    alpha= rho / dot(size, p, q);
    // x+= alpha * p; r-= alpha * q;
    for (i= 0; i < size; i++) {
        x[i]+= alpha * p[i];
        r[i]-= alpha * q[i];
    }
    iter++;
}

delete [] q; delete [] p; delete [] r; delete [] z;
return iter;
}

void ic_0(int size, double* out, double* in) { /* .. */ }
int main (int argc, char* argv[])
{
    int size=100;
    // set nnz and size
    double *x= new double[size];
    double *b= new double[size];
    for (int i=0; i<size; i++)
        b[i] = 1.0;
    for (int i=0; i<size; i++)
        x[i] = 0.0;
    // set A and b
    cg(size, x, b, diag_prec, 1e-9);
    return 0;
}
```

Let us discuss it in a general fashion. The good thing about this code is that it is self-contained—a virtue shared with much other bad code. However, this is about the only advantage. The problem with this implementation is its low abstraction level. This creates three major disadvantages:

- Bad readability,
- No flexibility, and
- High proneness to errors.

The bad readability manifests itself in the fact that almost every operation is implemented in one or multiple loops. For instance, would we have found the matrix vector multiplication q = Ap without the comments? Probably. We would easily catch where the variables representing q, A, and p are used, but to see that this is a matrix vector product takes a closer look and a good understanding of how the matrix is stored.

This leads us to the second problem: the implementation commits to many technical details and only works in precisely this context. Algorithm A-1 only requires that matrix A is symmetric positive-definite, but it does not demand a certain storage scheme, even less a specific matrix. Herbert implemented the algorithm for a matrix that represents a discretized 1D Poisson equation. Programming at such a low abstraction level requires modifications every time we have other data or other formats.

The matrix and its format are not the only details the code commits to. What if we want to compute in lower (float) or higher (long double) precision? Or solve a complex linear system? For every such new CG application, we need a new implementation. Needless to say, running on parallel computers or exploring GPGPU (General-Purpose Graphic Processing Units) acceleration needs reimplementations as well. Much worse, every combination of the above needs a new implementation.

Some readers might think: “It is only one function of 20 or 30 lines. Rewriting this little function, how much work can this be? And we do not introduce new matrix formats or computer architectures every month.” Certainly true, but in some sense it is putting the cart before the horse. Because of such inflexible and detail-obsessed programming style, many scientific applications grew into the hundred thousands and millions of lines of code. Once an application or library reaches such a monstrous size, it is arduous to modify features of the software and it is only rarely done. The road to success is starting software from a higher level of abstraction from the beginning, even when it is more work initially.

The last major disadvantage is how prone the code is to errors. All arguments are given as pointers, and the size of the underlying arrays is given as an extra argument. We as programmers of function cg can only hope that the caller did everything right because we have no way to verify it. If the user does not allocate enough memory (or does not allocate it at all), the execution will crash at some more or less random position or, even worse, will generate some nonsensical results because data and even the machine code of our program can be randomly overwritten. Good programmers avoid such fragile interfaces because the slightest mistake can have catastrophic consequences, and the program errors are extremely difficult to locate. Unfortunately, even recently released and widely used software is written in this manner, either for backward compatibility to C and Fortran or because it is written in one of these two languages. Or the developers are just resistant to any progress in software development. In fact, the implementation above is C and not C++. If this is how you like software, you probably will not like this book.

So much about software we do not like. In Listing A-2, we show a version that comes much closer to our ideal.

## Listing A-2: High-abstraction implementation of CG

```cpp
template < typename Matrix, typename Vector,
typename Preconditioner >
int conjugate_gradient( const Matrix& A, Vector& x, const Vector& b,
const Preconditioner& L, const double& eps)
{
typedef typename Collection<Vector>::value_type Scalar;
Scalar rho= 0, rho_1= 0, alpha= 0;
Vector p(resource(x)), q(resource(x)), r(resource(x)),
z(resource(x));
r= b - A * x;
int iter = 0;

while (one_norm(size, r) >= eps) {
    prec(r, z);
    rho = dot(r, z);

    if (iter.first())
        p = z;
    else
        p = z + (rho / rho_i) * p;
    q = A * p;
    alpha = rho / dot(p, q);

    x += alpha * p;
    r -= alpha * q;
    rho_i = rho;
    ++iter;
}

return iter;
}

int main (int argc, char* argv[])
{
    // initiate A, x, and b
    conjugate_gradient(A, x, b, diag_prec, 1.e-5);
    return 0;
}
```

The first thing you might realize is that the CG implementation is readable without comments. As a rule of thumb, if other people's comments look like your program sources, then you are a really good programmer. If you compare the mathematical notation in Algorithm A-1 with Listing A-2 you will realize that—except for the type and variable declarations at the beginning—they are identical. Some readers might think that it looks more like MATLAB or Mathematica than C++. Yes, C++ can look like this if one puts enough effort into good software.

Evidently, it is also much easier to write algorithms at this abstraction level than expressing them with low-level operations.

## The Purpose of Scientific Software

Scientists do research. Engineers create new technology.

Excellent scientific and engineering software is expressed only in mathematical and domain-specific operations without any technical detail exposed.

At this abstraction level, scientists can focus on models and algorithms, thus being much more productive and advancing scientific discovery.

Nobody knows how many scientists are wasting how much time every year dwelling on small technical details of bad software like Listing A-1. Of course, the technical details have to be realized in some place but not in a scientific application. This is the worst possible location. Use a two-level approach: write your applications in terms of expressive mathematical operations, and if they do not exist, implement them separately. These mathematical operations must be carefully implemented for absolute correctness and optimal performance. What is optimal depends on how much time you can afford for tuning and on how much benefit the extra performance gives you. Investing time in your fundamental operations pays off when they are reused very often.

### Advice

Use the right abstractions!
If they do not exist, implement them.

Speaking of abstractions, the CG implementation in Listing A-2 does not commit to any technical detail. In no place is the function restricted to a numerical type like double. It works as well for float, GNU’s multiprecision, complex, interval arithmetic, quaternions, ...

The matrix A can be stored in any internal format, as long as A can be multiplied with a vector. In fact, it does not even need to be a matrix but can be any linear operator. For instance, an object that performs a Fast Fourier Transformation (FFT) on a vector can be used as A when the FFT is expressed by a product of A with the vector. Similarly, the vectors do not need to be represented by finite-dimensional arrays but can be elements of any vector space that is somehow computer-representable as long as all operations in the algorithm can be performed.

We are also open to other computer architectures. If the matrix and the vectors are distributed over the nodes of a parallel supercomputer and corresponding parallel operations are available, the function runs in parallel without changing any single line. (GP)GPU acceleration can also be realized without changing the algorithm’s implementation. In general, any existing or new platform for which we can implement matrix and vector types and their corresponding operations is supported by our Generic conjugate gradient function.

As a consequence, sophisticated scientific applications of several thousand lines on top of such abstractions can be ported to new platforms without code modification.

## A.2 Basics in Detail

This section accumulates the outsourced details from Chapter 1.

### A.2.1 More about Qualifying Literals

Here we want to expand the examples for literal qualifications from Section 1.2.2 a bit.

**Availability:** The standard library provides a (template) type for complex numbers where the type for the real and imaginary parts can be parameterized by the user:

```cpp
std::complex<float> z(1.3, 2.4), z2;
```
