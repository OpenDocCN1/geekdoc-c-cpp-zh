```
{
  m_data = new int[length];
}
~IntArray()
{
  delete[] m_data;
}
int& operator[](int index)
{
  return m_data[index];
}
int getLength() { return m_length; }

```

```
int main()
{
IntArray array { 5, 4, 3, 2, 1 };
}
```

// output
error: no matching function for call to 'IntArray::IntArray<brace-enclosed initializer list>'

In this example the brace initialization IntArray array { 5, 4, 3, 2, 1 } will not compile because the IntArray class does not have a constructor that can handle initializer lists.

In C++11, when a compiler uses a braced initializer list, it implicitly converts it into an object of type std::initializer_list<T>. All STL containers have a constructor that takes an initializer list as a parameter. This enables vectors and other containers to support brace initialization.

Prior to C++11, the only way to initialize a vector would have been as follows:

```
std::vector<int> vec1;
for(int i = 0; i < 5; i++)
vec1.push_back(i);
```

However since C++11, std::vector contains a constructor for initializer lists, so we can