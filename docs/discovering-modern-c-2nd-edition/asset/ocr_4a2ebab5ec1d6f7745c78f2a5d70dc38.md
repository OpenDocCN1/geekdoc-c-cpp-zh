```
template <typename T>
struct list
{
  // previous contents...
  list_iterator<T> begin() { return list_iterator<T>(first); }
  list_iterator<T> end() { return list_iterator<T>(0); }
}
```