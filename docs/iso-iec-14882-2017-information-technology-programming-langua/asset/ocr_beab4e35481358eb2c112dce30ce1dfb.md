# ISO/IEC 14882:2017(E)

(19.1) —— operation_not_permitted — if pm is nullptr.

(19.2) —— resource_deadlock_would_occur — if entry owns is true.

```
void unlock() {
  Effects: As if by pm->unlock_shared();
  Postconditions: owns == false;
  Throws: system_error when an exception is required (33.2.2).
  Error conditions:
```

(23.1) —— operation_not_permitted — if entry owns is false.

# 33.4.4.3 shared_lock modifiers

```
void swap(shared_lock& sl) noexcept {
  Effects: Swaps the data members *this and sl.
  mutex_type* release() noexcept {
  Returns: The previous value of pm.
  Postconditions: pm == nullptr and owns == false;
```

```
template <class Mutex>
void swap(shared_lock<Mutex>& x, shared_lock<Mutex>& y) noexcept {
  Effects: As if x.swap(y);
```

# 33.4.4.4 shared_lock observers

```
bool owns_lock() const noexcept {
  Returns: owns.
  explicit operator bool() const noexcept {
  Returns: owns.
mutex_type* mutex() const noexcept {
  Returns: pm;
```

# 33.4.5 Generic locking algorithms

```
template <class L1, class L2, class L3...> int try_lock(L1&, L2&, L3&...);
```

Requires: Each template parameter type shall meet the Lockable requirements. [Note: The Unique_lock class template meets these requirements when instantly instantiated. — end note]

Effects: Calls try_lock() for each argument beginning with the first until all arguments have been processed or a call to try_lock() fails, either by returning false or throwing an exception. If a call to try_lock() fails, unlock() shall be called for all prior arguments and there should be no further calls to try_lock().

Returns: -1 if all calls to try_lock() returned true, otherwise a zero-based index value that indicates the argument for which try_lock() returned false.