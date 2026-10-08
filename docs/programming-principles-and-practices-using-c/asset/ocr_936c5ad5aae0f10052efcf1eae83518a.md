| Selected standard algorithms |
| :--- |
| **equal**(b,e,b2) | Do all elements of [**b:e**) and [**b2:b2+(e-b)**) compare equal? |
| **x=accumulate**(b,e,i) | **x** is the sum of **i** and the elements of [**b:e**). |
| **x=accumulate**(b,e,i,op) | Like the other **accumulate**, but with the “sum” calculated using **op**. |
| **x=inner_product**(b,e,b2,i) | **x** is the inner product of [**b:e**) and [**b2:b2+(e-b)**). |
| **x=inner_product**(b,e,b2,i,op,op2) | Like the other **inner_product**, but with **op** and **op2** instead of **+** and **\*.** |

By default, comparison for equality is done using **==** and ordering is done based on **<** (less than). The standard library algorithms are found in **<algorithm>**. For more information, see §5.5 and the sources listed in §21.2–21.5. These algorithms take one or more sequences. An input sequence is defined by a pair of iterators; an output sequence is defined by an iterator to its first element. Typically an algorithm is parameterized by one or more operations that can be defined as function objects or as functions. The algorithms usually report “failure” by returning the end of an input sequence. For example, **find**(b,e,v) returns **e** if it doesn’t find **v**.

# ## 21.2 The simplest algorithm: find()

Arguably, the simplest useful algorithm is **find**(). It finds an element with a given value in a sequence:

```
```cpp
template<typename In, typename T>
  // requires Input_iterator<In>()
  //      && Equality_comparable<Value_type<T>>() (§19.3.3)
In find(In first, In last, const T& val)
  // find the first element in [first,last) that equals val
{
  while (first!=last && *first != val) ++first;
  return first;
}
```
```

Let’s have a look at the definition of **find**(). Naturally, you can use **find**() without knowing exactly how it is implemented – in fact, we have used it already (e.g., §20.6.2). However, the definition of **find**() illustrates many useful design ideas, so it is worth looking at.

First of all, **find**() operates on a sequence defined by a pair of iterators. We are looking for the value **val** in the half-open sequence [**first:last**). The result returned