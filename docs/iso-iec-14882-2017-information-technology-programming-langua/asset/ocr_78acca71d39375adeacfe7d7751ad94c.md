# ISO/IEC 14882:2017(E)

# 23.18.3  type_index members

type_index(const type_info& rhs) noexcept;

+   1 Effects: Constructs a type_index object, the equivalent of target = &rhs.

+   2 bool operator=(const type_index& rhs) const noexcept;

+   Returns: *target == *rhs.target.

+   3 bool operator!(const type_index& rhs) const noexcept;

+   Returns: target != *rhs.target.

+   4 bool operator<(const type_index& rhs) const noexcept;

+   Returns: target->before(*target).

+   5 bool operator>(const type_index& rhs) const noexcept;

+   Returns: rhs->target->before(*target).

+   6 bool operator==(const type_index& rhs) const noexcept;

+   Returns: rhs->target->before(*target).

+   7 bool operator<=(const type_index& rhs) const noexcept;

+   Returns: target->before(*rhs.target).

size_t hash_code() const noexcept;

Returns: target->hash_code().

const char* name() const noexcept;

Returns: target->name().

# 23.18.4 Hash support

```
template < struct hash_type>;
```

+   1 For an object index of type_index, hash<type_index>(index) shall evaluate to the same result as index.hash_code().

# 23.19 Execution policies

# 23.19.1 In general

+   1 This subclause describes that execution policy types. An object of an execution policy indicates the kind of parallelism allowed in the execution of an algorithm and expresses the requirements on the element access functions. Example:

```
using namespace std;
vector<int> v = / ... /

// standard sequential sort
sort(v.begin(), v.end());

// explicitly sequential sort
sort(execution:seq, v.begin(), v.end());

// permitting parallel execution
sort(execution:par, v.begin(), v.end());
```