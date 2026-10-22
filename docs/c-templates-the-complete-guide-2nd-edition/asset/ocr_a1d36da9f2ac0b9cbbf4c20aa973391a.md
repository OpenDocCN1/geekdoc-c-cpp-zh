```
};

template<typename T, std::size_t N>
struct IsArrayT<T[N]> : std::true_type { //partial specialization for arrays
using BaseT = T;
static constexpr std::size_t size = N;
};
```

```
template<typename T>
struct IsArrayT<T[]> : std::true_type { //partial specialization for unbound arrays
using BaseT = T;
static constexpr std::size_t size = 0;
};
```

Here, multiple additional members provide information about the arrays being classified: their base type and their size (with 0 used to denote an unknown size).

The C++ standard library provides the corresponding trait std::is_array<> to check whether a type is an array, which is described in Section D.2.1 on page 704. In addition, traits such as std::rank<> and std::extent<> allow us to query their number of dimensions and the size of a specific dimension (see Section D.3.1 on page 715).

# Pointers to Members

Pointers to members can be treated using the same technique: Click here to view code image

traits/ispointertomember.hpp

```
template<typename T>
struct IsPointerToMemberT : std::false_type { //by default no pointer-to-member
};
```

```
template<typename T, typename C>
struct IsPointerToMemberT<T C::*> : std::true_type { //partial specialization
using MemberT = T;
using ClassT = C;
};
```

Here, the additional members provide both the type of the member and the type of the class in which that member occurs.

The C++ standard library provides more specific traits,