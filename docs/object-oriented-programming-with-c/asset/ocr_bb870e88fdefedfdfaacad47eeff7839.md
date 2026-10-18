Consider a vector class defined as follows:

```
class vector
{
    int *v;
    int size;
    public:
    vector(int m)    // create a null vector
    {
    v = new int[size = m];
    for(int i=0; i<size; i++)
    v[i] = 0;
    }
    vector(int *a)    // create a vector from an array
    {
    for(int i=0; i<size; i++)
    v[i] = a[i];
    }
    int operator*(vector &y)    // scalar product
    {
    int sum = 0;
    for(int i=0; i<size; i++)
    sum += this -> v[i] * y . v[i];
    return sum;
    }
};
```

The vector class can store an array of int numbers and perform the scalar product of two int vectors as shown below:

```
int main()
{
    int x[3] = {1,2,3};
    int y[3] = {4,5,6};
    vector v1(3);    // Creates a null vector of 3 integers
    vector v2(3);
};
```