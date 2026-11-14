```
v2w is [(2,0), (3,0)]
v2c is [(2,3)]
v2dw is [(2,3)]

v3 is [(2,0), (3,0), (4,0)]
v3d is [(2,0), (3,0), (4,0)]
v3dc is [(2,3), (4,0)]
```

All this said, we have to pay attention that the initialization of nested data is really performed as we intended. It is also worthwhile to reflect on the most comprehensible notation, especially when we share our sources with other people.

Uniform initialization favors constructors for `initializer_list<>` , and many other constructors are hidden in the brace notation. As a consequence, we cannot replace all parentheses with braces in constructors and expect the same behavior:

```
vector_complex v1(7);
vector_complex v2{7};
```

The first vector has seven entries with value 0 and the second vector one entry with value 7.

# ## A.4.3 Accessing Multi-dimensional Arrays

Let us assume that we have a simple class like the following:

```
class matrix
{
public:
	matrix(int nrows, int ncols)
	: nrows(nrows), ncols(ncols), data( new double[nrows * ncols] ) {}

	matrix(const matrix& that)
	: nrows(that.nrows), ncols(that.ncols),
	data(new double[nrows * ncols])
	{
	for (int i = 0, size= nrows*ncols; i < size; ++i)
	data[i] = that.data[i];
	}

	void operator=(const matrix& that)
	{
	assert(nrows == that.nrows && ncols == that.ncols);
	for (int i = 0, size= nrows*ncols; i < size; ++i)
	data[i] = that.data[i];
	}

	int num_rows() const { return nrows; }
	int num_cols() const { return ncols; }

private:
	int nrows, ncols;
	unique_ptr<double> data;
};
```