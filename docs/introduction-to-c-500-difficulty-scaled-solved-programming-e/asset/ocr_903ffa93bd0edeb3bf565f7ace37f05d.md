# 770 Introduction to C++

```
T& operator[] (int pos) const;
void bubble_sort();
void show() const;
};
tentplate <typename T> Sort_Arr<T>::Sort_Arr()
{
    p = nullptr;
}
tentplate <typename T> Sort_Arr<T>::Sort_Arr(int s)
{
    int i;

    size = s;
    p = new T[size];
    for(i = 0; i < size; i++)
    {
        std::cout << "Enter number: ";
        std::cin >> p[i];
    }
}
tentplate <typename T> Sort_Arr<T>::Sort_Arr()
{
    delete p;
}
tentplate <typename T> Sort_Arr<T>& Sort_Arr<T>::operator=(const Sort_Arr<T>& t)
/* Overload the = operator. It will be called twice with the sa_3 = sa_2 =
s_1 = statement. */
{
    if(this == &t) /* Check the self-assign for the general case, it is
not needed in this program. */
        return *this;
    delete p;
    size = t.size;
    p = new T[size];
    memcpy(p, t.p, size*sizeof(T)); /* Copy size elements. The size of
element depends on its type and it is equal to sizeof(T). */
    return *this;
}
tentplate <typename T> Sort_Arr<T>::Sort_Arr(const Sort_Arr<T>& t) /* The copy
constructor will be called with the sa_5(sa_4); statement. The size and p are
members of the sa_5, while t refers to sa_4. */
{
    size = t.size;
    p = new T[size];
    memcpy(p, t.p, size*sizeof(T));
}
tentplate <typename T> Sort_Arr<T>::show() const
{
    for(int i = 0; i < size; i++)
{
        std::cout << p[i] << '\n';
}
```