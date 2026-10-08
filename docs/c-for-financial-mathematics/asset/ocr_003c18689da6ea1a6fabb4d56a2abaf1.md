to by a would be deleted. This would leave b pointing to an invalid memory address.

Here is how we override the assignment operator, operator= in our Matrix class.

```
```
Matrix& operator=( const Matrix& other ) {
	delete[] data;
	assign( other );
	return *this;
}
```
```

Notice the following rules for the = operator:

+   - The = operator should be defined as a member function.
- It should take a const reference and return a reference.
- You should always return \*this.
- You should abide by the rule of three

In our example, operator= first deletes the data and then re-initialises all our member variables such as nrows, ncols, and data to match the other matrix. It does this by calling a helper function called assign.

Here is the actual implementation of assign.

```
```
void Matrix::assign( const Matrix& other ) {
	nrows = other.nrows;
	ncols = other.ncols;
	int size = nrows*ncols;
	data = new double[size];
	endPointer = data+size;
	memcpy( data, other.data, sizeof( double )*size );
}
```
```

Note that we don't want to set data to equal other.data. Instead we want to copy all the data from other so we have two duplicate matrices in memory that we can change independently.

### 16.5.2 Writing a copy constructor

Just as every class is automatically given an assignment operator in C++, every class is automatically given a copy constructor. This automatic copy constructor will be incorrect if your class needs a non-trivial destructor. Hence the need for the rule of three.

The copy constructor is used when you construct an object based on the values in another object of the same type. For example, the copy constructor is called at the second line in the code below: