provided by a constant function. What we are missing is access to the matrix entries.

> Be Aware!
> The bracket operator accepts only one argument.

That means we cannot define:

```
double& operator[] (int r, int c) { ... }
```

# A.4.3.1 Approach 1: Parentheses

The simplest way to handle multiple indices is replacing the square brackets with parentheses:

Click here to view code image

```
double& operator() (int r, int c)
{
    return data[r*ncols + c];
}
```

Adding range checking—in a separate function for better reuse—can save us a lot of debug time in the future. We also implement the constant access:

Click here to view code image

```
private:
    void check(int r, int c) const { assert(0 <= r && r < nrows
    &&
    0 <= c && c <
    ncols); }
public:
    double& operator() (int r, int c)
    {
        check(r, c);
        return data[r*ncols + c];
    }
    const double& operator() (int r, int c) const
    {
        check(r, c);
        return data [r*ncols + c];
    }
```

The access of matrix entries is accordingly denoted with parentheses: