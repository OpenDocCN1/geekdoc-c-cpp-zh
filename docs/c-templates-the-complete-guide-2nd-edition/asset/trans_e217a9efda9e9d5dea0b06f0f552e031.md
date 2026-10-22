
整数值的乘积为 0

# traits/sumpolicy2.hpp

```cpp
#ifndef SUMPOLICY_HPP
#define SUMPOLICY_HPP

template<typename T1, typename T2>
class SumPolicy {
 public:
   static void accumulate (T1& total, T2 const& value) {
       total += value;
   }
};

#endif // SUMPOLICY_HPP
```

traits/accum7.hpp

```
#ifndef ACCUM_HPP
#define ACCUM_HPP

#include "accumtraits4.hpp"
#include "sumpolicy2.hpp"

template<typename T,
    template<typename,typename> class Policy = SumPolicy,
    typename Traits = AccumulationTraits<T>>
auto accum (T const* beg, T const* end)
{
    using AccT = typename Traits::AccT;
    AccT total = Traits::zero();
    while (beg != end) {
        Policy<AccT,T>::accumulate(total, *beg);
        ++beg;
    }
    return total;
}

#endif //ACCUM_HPP
```

traits/accum0.hpp

```
#ifndef ACCUM_HPP
#define ACCUM_HPP

#include <iterator>

template<typename Iter>
auto accum (Iter start, Iter end)
{
    using VT = typename std::iterator_traits<Iter>::value_type;

    VT total{};  // assume this actually creates a zero value
    while (start != end) {
        total += *start;
        ++start;
    }
    return total;
}

#endif // ACCUM_HPP
```

```cpp
#include <cstddef>
#include <iostream>

template<typename T>
struct TypeSize {
    static std::size_t const value = sizeof(T);
};

int main()
{
    std::cout << "TypeSize<int>::value = "
              << TypeSize<int>::value << '\n';
}
```

traits/elementtype.hpp

```
#include <vector>
#include <list>

template<typename T>
struct ElementT;                 // primary template

template<typename T>
struct ElementT<std::vector<T>> { // partial specialization for std::vector
    using Type = T;
};

template<typename T>
struct ElementT<std::list<T>> {   // partial specialization for std::list
    using Type = T;
};
...
```

# traits/elementtype.cpp

```cpp
#include "elementtype.hpp"
#include <vector>
#include <iostream>
#include <typeinfo>

template<typename T>
void printElementType (T const& c)
{
    std::cout << "Container of "
              << typeid(typename ElementT<T>::Type).name()
              << " elements.\n";
}

int main()
{
    std::vector<bool> s;
    printElementType(s);
    int arr[42];
    printElementType(arr);
}
```

```
template<typename T1, typename T2, ...>
class X {
    public:
        using ... = T1;
        using ... = T2;
        ...
};
```

```
template<typename C>
typename ElementT<C>::Type sumOfElements (C const& c);
```

```
template<typename T>
using ElementType = typename ElementT<T>::Type;
```

```
template<typename C>
ElementType<C> sumOfElements (C const& c);
```

```
template<typename T>
using RemoveReference = typename RemoveReference<T>::Type;
```

traits/addreference.hpp

```
template<typename T>
struct AddLValueReferenceT {
    using Type = T&;
};

template<typename T>
using AddLValueReference = typename AddLValueReferenceT<T>::Type;

template<typename T>
struct AddRValueReferenceT {
    using Type = T&&;
};

template<typename T>
using AddRValueReference = typename AddRValueReferenceT<T>::Type;
```

```
template<typename T>
using AddLValueReferenceT = T&;

template<typename T>
using AddRValueReferenceT = T&&;
```

```cpp
template<>
struct AddLValueReferenceT<void> {
    using Type = void;
};

template<>
struct AddLValueReferenceT<void const> {
    using Type = void const;
};

template<>
struct AddLValueReferenceT<void volatile> {
    using Type = void volatile;
};

template<>
struct AddLValueReferenceT<void const volatile> {
    using Type = void const volatile;
};
```

traits/removeconst.hpp

```
template<typename T>
struct RemoveConstT {
    using Type = T;
};

template<typename T>
struct RemoveConstT<T const> {
    using Type = T;
};

template<typename T>
using RemoveConst = typename RemoveConstT<T>::Type;
```

traits/removecv.hpp

```
#include "removeconst.hpp"
#include "removevolatile.hpp"

template<typename T>
struct RemoveCVT : RemoveConstT<typename RemoveVolatileT<T>::Type> {
};

template<typename T>
using RemoveCV = typename RemoveCVT<T>::Type;
```

```
template<typename T>
using RemoveCV = RemoveConst<RemoveVolatile<T>>;
```

```
template<typename R, typename... Args>
struct DecayT<R(Args...)> {
    using Type = R (*)(Args...);
};
```

```
template<typename R, typename... Args>
struct DecayT<R(Args..., ...)> {
    using Type = R (*)(Args..., ...);
};
```

traits/decay.cpp

```
#include <iostream>
#include <typeinfo>
#include <type_traits>
#include "decay.hpp"

template<typename T>
void printDecayedType()
{
    using A = typename DecayT<T>::Type;

    std::cout << "Parameter type: " << typeid(A).name() << '\n';
    std::cout << "- is int:       " << std::is_same<A,int>::value << '\n';
    std::cout << "- is const:     " << std::is_const<A>::value << '\n';
    std::cout << "- is pointer: " << std::is_pointer<A>::value << '\n';
}

int main()
{
    printDecayedType<int>();
    printDecayedType<int const>();
    printDecayedType<int[7]>();
    printDecayedType<int(int)>();
}
```

```cpp
template <typename T>
using Decay = typename Decay<T>::Type;
```

traits/issame0.hpp

```
template<typename T1, typename T2>
struct IsSameT {
    static constexpr bool value = false;
};

template<typename T>
struct IsSameT<T, T> {
    static constexpr bool value = true;
};
```

```
if (IsSameT<T, int>::value) ...
```

traits/boolconstant.hpp

```
template<bool val>
struct BoolConstant {
    using Type = BoolConstant<val>;
    static constexpr bool value = val;
};
using TrueType  = BoolConstant<true>;
using FalseType = BoolConstant<false>;
```

traits/issame.hpp

```
#include "boolconstant.hpp"

template<typename T1, typename T2>
struct IsSameT : FalseType
{
};

template<typename T>
struct IsSameT<T, T> : TrueType
{
};
```

traits/issame.cpp

```
#include "issame.hpp"
#include <iostream>

template<typename T>
void fooImpl(T, TrueType)
{
    std::cout << "fooImpl(T,true) for int called\n";
}

template<typename T>
void fooImpl(T, FalseType)
{
    std::cout << "fooImpl(T,false) for other type called\n";
}

template<typename T>
void foo(T t)
{
    fooImpl(t, IsSameT<T,int>{});  // choose impl. depending on whether T is int
}

int main()
{
    foo(42);    // calls fooImpl(42, TrueType)
    foo(7.7);   // calls fooImpl(42, FalseType)
}
```

```
template<typename T>
using IsSame = typename IsSameT<T>::Type;
```

```cpp
namespace std {
    using true_type = integral_constant<bool, true>;
    using false_type = integral_constant<bool, false>;
}
```

```
template<bool B>
using bool_constant = integral_constant<bool, B>;
```

```
template<typename T1, typename T2>
Array<typename PlusResultT<T1, T2>::Type>
operator+ (Array<T1> const&, Array<T2> const&);
```

```
template<typename T1, typename T2>
Array<PlusResult<T1, T2>>
operator+ (Array<T1> const&, Array<T2> const&);
```

```
class Integer { ... };
Integer const operator+ (Integer const&, Integer const&);
```

```
template<typename T1, typename T2>
Array<RemoveCV<RemoveReference<PlusResult<T1, T2>>>>
operator+ (Array<T1> const&, Array<T2> const&);
```

```
namespace std {
    template<typename T>
    add_rvalue_reference_t<T> declval() noexcept;
}
```

traits/plus2.hpp

```
#include <utility>

template<typename T1, typename T2>
struct PlusResultT {
    using Type = decltype(std::declval<T1>() + std::declval<T2>());
};

template<typename T1, typename T2>
using PlusResult = typename PlusResultT<T1, T2>::Type;
```

