```
DynamicArray& operator=(const DynamicArray& other)
{
  // Delete existing data
  delete[] mArray;
  // Copy from other
  mSize = other.mSize;
  mArray = new int[mSize];
  for (int i = 0; i < mSize; i++)
  {
    mArray[i] = other.mArray[i];
  }
  // By convention, return *this
  return *this;
}
```