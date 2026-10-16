```
```cpp
void my_algo(vector<Val>& vv) {
  using namespace std::rel_ops;
  for (int i=0; i<vv.size(); ++i)
    if (0>vv[i]) vv[i]=abs(vv[i]); // OK. > from rel_ops }
```
```

It can be hard to use **rel_ops** without polluting a namespace. In particular:

```
```cpp
namespace Mine {
  struct Val {
    double d;
    bool operator==(Val v) const { return v.d==d; }
  };
  using namespace std::rel_ops;
}
```
```

This could expose the perfectly general templates from **rel_ops** to be found by argument-dependent lookup (§14.2.4) and applied to types for which they may be inappropriate. A safer approach is to place **using**-directives in local scopes.

# 35.5.4 Comparing and Hashing **type_info**

In <typeindex>, the standard library provides support for comparing and hashing **type_index**. A **type_index** is created from a **type_info** (§22.5), specifically to allow such comparison and hashing. **type_index** Operations (§iso.20.13)

+   - `tip` is a pointer to the **type_info** represented by a **type_index**
+   - `type_index ti {tinf};` ti represents the **type_info** `tinf`; noexcept
+   - `ti==ti2` ti and ti2 represent the same **type_info**: `*ti.tip==*ti2.tip`; noexcept
+   - `ti!=ti2` !`(ti==ti2)`; noexcept
+   - `ti<ti2` `ti.tip->before(ti2.tip)`; noexcept
+   - `ti<=ti2` !`ti2.tip->before(ti.tip)`; noexcept
+   - `ti>ti2` `ti2.tip->before(ti.tip)`; noexcept
+   - `ti>=ti2` !`ti.tip->before(ti2.tip)`; noexcept
+   - `n=ti.hash_code()` `n=ti.tip->hash_code()`
+   - `p=name()` `p=ti.tip->name()`
+   - `hash<type_index>` A specialization of `hash` (§31.4.3.4)

For example:

**Section 35.5.4 Comparing and Hashing type_info 1031**

```
```cpp
unordered_map<type_index,type_info *> types; // …
types[type_index{something}] = &typeid(something);
```
```

# 35.6 Advice

+   1. Use <chrono> facilities, such as **steady_clock**, **duration**, and **time_point** for timing; §35.2.
+   2. Prefer <clock> facilities over <ctime> facilities; §35.2.
+   3. Use **duration_cast** to get durations in known units of time; §35.2.1.