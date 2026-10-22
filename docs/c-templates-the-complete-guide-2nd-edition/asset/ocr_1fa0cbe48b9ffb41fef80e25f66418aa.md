# 24.2.5 Transforming a Typelist

Our previous typelist algorithms have allowed us to extract arbitrary elements from a typelist, search within the list, construct new lists, and reverse lists. However, we have yet to perform any operations on the elements within the typelist. For example, we may want to “transform” all of the types in the typelist in some way,⁵ such as by turning each type into its const-qualified variant using the AddConst metafunction: Click here to view code image

typelist/addconst.hpp

```
template<typename T>
struct AddConstT
{
using Type = T const;
};

template<typename T>
using AddConst = typename AddConstT<T>::Type;
```

To that end, we will implement a Transform algorithm that takes a typelist and a metafunction and produces another typelist containing the result of applying the metafunction to each type. For example, the type Transform<SignedIntegralTypes, AddConstT> will be a typelist containing signed char const, short const, int const, long const, and long long const. The metafunction is provided through a template template parameter, which maps an input type to an output type. The Transform algorithm itself is, as we might expect, a recursive algorithm: Click here to view code image

typelist/transform.hpp

```
template<typename List, template<typename T> class MetaFun,
bool Empty = IsEmpty<List>::value>
class TransformT;

// recursive case:
template<typename List, template<typename T> class MetaFun>
class TransformT<List, MetaFun, false>

: public PushFrontT<typename TransformT<PopFront<List>, MetaFun>::Type,
typename MetaFun<Front<List>>::Type>
{
```