```
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
```

```
int main (int argc, char* argv[])
{
    // initiate A, x, and b
    conjugate_gradient(A, x, b, diag_prec, 1.e-5);
    return 0 ;
}
```

The first thing you might realize is that the CG implementation is readable without comments. As a rule of thumb, if other people's comments look like your program sources, then you are a really good programmer. If you compare the mathematical notation in Algorithm A-1 with Listing A-2 you will realize that—except for the type and variable declarations at the beginning—they are identical. Some readers might think that it looks more like MATLAB or Mathematica than C++. Yes, C++ can look like this if one puts enough effort into good software.

Evidently, it is also much easier to write algorithms at this abstraction level than expressing them with low-level operations.

# The Purpose of Scientific Software

Scientists do research. Engineers create new technology.

Excellent scientific and engineering software is expressed only in mathematical and domain-specific operations without any technical detail exposed.

At this abstraction level, scientists can focus on models and algorithms, thus being much more productive and advancing scientific discovery.

Nobody knows how many scientists are wasting how much time every year dwelling on small technical details of bad software like Listing A-1. Of course, the technical details have to be realized in some place but not in a scientific application. This is the worst possible