```
}
Person (T2 t2, T1 t1)
{
    m_t2 = t2;
    m_t1 = t1;
    cout << m_t1 << " " << m_t2 << endl;
}
};
void main()
{
    Person<int, float> objPerson1(1, 2.345);
    Person<float, char> objPerson2(2.132, 'r');
}
```

# 12.3 Identify the error in the following program.

```
#include <iostream.h>

template <class T1, class T2>
T1& MinMax(T1 t1, T2 t2)
{
    return t1 > t2 ? t1 : t2;
    cout << "";
}
void main()
{
    cout << ++MinMax(2, 3);
}
```

# 12.4 Find errors, if any, in the following code segment.

```
template<class T>
T max(T, T)
{.....};
unsigned int m;
int main()
{
```