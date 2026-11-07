# **Program 18.10**  File `queue.cpp` (Continued)

```
```cpp
// Definition of pop operation
template <typename T>
void Queue<T>::pop()
{
    list.erase (0);
}

// Definition of front operation
template <typename T>
T& Queue<T>::front() const
{
    return list.get (0);
}
// Definition of back operation
template <typename T>
T& Queue<T>::back() const
{
    return list.get (list.size () - 1);
}
// Definition of size operation
template <typename T>
int Queue<T>::size () const
{
    return list.size ();
}
// Definition of print operation
template <typename T>
void Queue<T>::print () const
{
    list.print ();
}
#endif
```
```

**Application File** We use a very simple application to test the interface and implementation file, as shown in Program 18.11.

# **Program 18.11**  Application file for testing the Queue class

```
```cpp
/*******************************************************
 * The application to test the Queue class              *
 *******************************************************/
#include "queue.cpp"

int main ( )
{
```
```