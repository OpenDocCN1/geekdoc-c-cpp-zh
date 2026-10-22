```
// assign stack of elements of type T2
template<typename T2,
    template<typename Elem2,
        typename = std::allocator<Elem2>
    >class Cont2>
Stack<T,Cont>& operator= (Stack<T2,Cont2> const&);
// to get access to private members of any Stack with elements of type T2:
template<typename, template<typename, typename>class>
friend class Stack;
};

template<typename T, template<typename,typename> class Cont>
void Stack<T,Cont>::push (T const& elem)
{
    elems.push_back(elem);    // append copy of passed elem
}

template<typename T, template<typename,typename> class Cont>
void Stack<T,Cont>::pop ()
{
```