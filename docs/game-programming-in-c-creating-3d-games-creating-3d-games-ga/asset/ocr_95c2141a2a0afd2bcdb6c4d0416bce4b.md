```
friend bool operator==(const Complex& a, const Complex& b)
{
    return (a.mReal == b.mReal) &&
           (a.mImaginary == b.mImaginary);
}
```