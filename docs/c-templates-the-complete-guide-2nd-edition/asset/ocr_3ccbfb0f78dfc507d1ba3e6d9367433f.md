the most general function template (the first swap()), and ensuring that the more specialized function template was also more specialized based on C++’s partial ordering rules.

Not all conceptually more specialized algorithm variants can be directly translated into function templates that provide the right partial ordering behavior. For our next example, consider However, the alternative presented here is more broadly applicable.

the advanceIter() function (similar to std::advance() from the C++ standard library), which moves an iterator x forward by n steps. This general algorithm can operate on any input iterator: Click here to view code image

```
template<typename InputIterator, typename Distance>
void advanceIter(InputIterator& x, Distance n)
{
while (n > 0) { //linear time
++x;
--n;
}
}
```

For a certain class of iterators—those that provide random access operations—we can provide a more efficient implementation: Click here to view code image

```
template<typename RandomAccessIterator, typename Distance>
void advanceIter(RandomAccessIterator& x, Distance n) {
 x += n; // constant time
}
```

Unfortunately, defining both of these function templates will result in a compiler error, because— as noted in the introduction—function templates that differ only based on their template parameter names are not overloadable. The remainder of this chapter will discuss techniques that emulate the desired effect of overloading these function templates.

# 20.2 Tag Dispatching

One approach to algorithm specialization is to “tag” different implementation variants of an algorithm with a unique type that identifies that variant. For example, to deal with the advanceIter() problem, just introduced, we can use the standard library’s iterator category tag types (defined below) to identify the two implementation variants of the advanceIter() algorithm: Click here