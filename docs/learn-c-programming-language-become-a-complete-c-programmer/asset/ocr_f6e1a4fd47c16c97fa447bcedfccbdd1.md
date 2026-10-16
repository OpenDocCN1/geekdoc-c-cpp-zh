For the move assignment, we can simply do a swap. The idea behind using a swap to implement a move assignment is that the source is just about to be destroyed, so we can just let the destructor for the source do the necessary cleanup work for us:

```
template<class T>
Matrix<T>& Matrix<T>::operator=(Matrix&& a) // moveassignment {
swap(dim,a.dim); // swaprepresentations
swap(elem,a.elem);
return *this;
}
```

Move constructors and move assignments take nonconst (rvalue) reference arguments: they can, and usually do, write to their argument. However, the argument of a move operation must always be left in a state that the destructor can cope with (and preferably deal with very cheaply and easily).

For resource handles, move operations tend to be significantly simpler and more efficient than copy operations. In particular, move operations typically do not throw exceptions; they don’t acquire resources or do complicated operations, so they don’t need to. In this, they differ from many copy operations (§17.5).

How does the compiler know when it can use a move operation rather than a copy operation? In a few cases, such as for a return value, the language rules say that it can (because the next action is defined to destroy the element). However, in general we have to tell it by giving an rvalue reference argument. For example:

```
template<class T>
void swap(T& a, T& b) // "perfect swap" (almost)
{
T tmp = std::move(a);
a = std::move(b);
b = std::move(tmp);
}
```

The move() is a standard-library function returning an rvalue reference to its argument (§35.5.1): move(x) means “give me an rvalue reference to x.” That is, std::move(x) does not move anything; instead, it allows a user to move x. It would have been better if move() had been called rval(),but the name move() has been used for this operation for years.

Standard-library containers have move operations (§3.3.2, §35.5.1) and so have other standardlibrary types, such as pair (§5.4.3, §34.2.4.1) and unique_ptr (§5.2.1, §34.3.1). Furthermore, operations that insert new elements into standard-library containers, such as insert() and push_back(), have versions that take rvalue references (§7.7.2). The net result is that the standard containers and algorithms deliver better performance than they would have been able to if they had to copy.

What if we try to swap objects of a type that does not have a move constructor? We copy and pay the price. In general, a programmer is responsible for avoiding excessive copying.