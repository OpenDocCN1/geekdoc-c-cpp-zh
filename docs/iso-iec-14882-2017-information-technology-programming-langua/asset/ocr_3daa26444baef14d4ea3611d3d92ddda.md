# ISO/IEC 14882:2017(E)

```
template<class Y> weak_ptr operator=(const weak_ptr<Y>& r) noexcept;
template<class Y> weak_ptr operator=(const shared_ptr<Y>& r) noexcept;
```

+   1 Effects: Equivalent to weak_ptr(r).*

+   2 Remarks: The implementation may meet the effects (and the implied guarantees) via different means, without creating a temporary.

+   3 Returns: *this.*

```
weak_ptr operator=(weak_ptr&& r) noexcept;
template<class Y> weak_ptr operator=(const weak_ptr<Y>& r) noexcept;
```

+   4 Effects: Equivalent to weak_ptr(std::move(r)).*

+   5 Returns: *this.*

# 23.11.2.3 weak_ptr modifiers [util.smartptr.weak]

```
void swap(weak_ptr& r) noexcept;
```

+   1 Effects: Exchanges the contents of *this and r.

+   2 void reset() noexcept;

+   2 Effects: Equivalent to weak_ptr<>().swap(*this).

# 23.11.2.5 weak_ptr observers [util.smartptr.weak.obs]

```
long use_count() const noexcept;
```

+   1 Returns: 0 if this is empty; otherwise, the number of shared_ptr<T> instances that share ownership with *this.

```
bool expired() const noexcept;
```

+   2 Returns: use_count() == ..

```
shared_ptr<T> lock() const noexcept;
template<class U> bool owner_before(const shared_ptr<U>& b) const;
template<class U> bool owner_before(const weak_ptr<U>& b) const;
```

+   3 Returns: expired() ? shared_ptr<T>(*this) : _, executed atomically.

+   4 Returns: An unspecified value such that

+   - x.owner_before(y) defines a relation defined by owner_before(b) && !b.owner_before(a) in 28;

+   (4.2) under the relation defined by owner_before, !a.owner_before(b) && !b.owner_before(a), two shared_ptr or weak_ptr instances are equivalent if they share ownership or both

# 23.11.2.6 weak_ptr specialized algorithms [util.smartptr.weak.spec]

```
template<class T>
void swap(weak_ptr<T>& a, weak_ptr<T>& b) noexcept;
```

+   Effects: Equivalent to a.swap(b).

# 23.11.2.4 Class template owner_less [util.smartptr.ownerless]

+   The class template owner_less allows ownership-mixed comparisons of shared and weak pointers.

```
namespace std {
template<class T> void lock() struct owner_less;
```

§ 23.11.2.4

©ISO/IEC 2017 - All rights reserved 630