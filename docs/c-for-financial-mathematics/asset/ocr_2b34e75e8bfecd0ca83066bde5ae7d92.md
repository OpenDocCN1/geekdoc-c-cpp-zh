You can use `new[]` with other data types too. To illustrate this let’s introduce a simple class, `Pair`.

```
```
class Pair {
public:
    double x;
    double y;
    Pair();
    Pair( double x, double y );
};
```
```

We assume that the default constructor of `Pair` initialises $x$ and $y$ to zero. Given this class, the code below creates a chunk of memory containing pairs. This time each pair is initialised to (0,0) since `Pair` has a default constructor.

```
```
int n = 5;
Pair* myPairs = new Pair[n];
for ( int i=0; i<n; i++ ) {
    double xValue = myPairs[i].x;
    double yValue = myPairs[i].y;
    
    cout<<"Pair (";
    cout<< xValue;
    cout<<",";
    cout<< yValue;
    cout<<")\n";
}
delete[] myPairs;
```
```

The type is a `Pair*`. This should be read “as a pointer to a `Pair`”.

# ### 11.2.2 Pointer operators

A pointer is just the address in memory of some data. On a 32-bit computer a pointer will be 4 bytes long. On a 64-bit computer it will be 8 bytes long. This means a 32-bit computer can have up to $2^{32}$bytes $\approx$ 2Gb of memory. 64-bit computers could in principle have vastly more memory. It is normal to write memory addresses as a hexadecimal number; e.g., **9ABF0132** is a typical memory address.

Consider the following code:

```
```
int* fivePrimes = new int[5];
fivePrimes[0] = 2;
fivePrimes[1] = 3;
fivePrimes[2] = 5;
fivePrimes[3] = 7;
fivePrimes[4] = 11;
```
```