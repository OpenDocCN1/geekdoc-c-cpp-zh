# ISO/IEC 14882:2017(E)

```
struct notrow_t { explicit notrow_t() = default; };nextern const notrow_t notrow;

hander operator new()();
```

```
using new_handler = void (*)(();)
new_handler get_new_handler() noexcept;
new_handler set_new_handler(new_handler new_p) noexcept;
```

```
// 21.6.4. pointer optimization barrier
template <class T> const T* launcher(T* p) noexcept
```

```
// 21.6.5. hardware interference size
inline const_t std::hardware_destructive_interference_size = defined;
inline const_t std::hardware_destructive_interference_size = defined;
```

```
void* operator new(size_t size);
void* operator new(size_t size, std::align_val alignment);
void* operator new(size_t size, const std::size_t size) noexcept;
void* operator new(size_t size, std::align_val alignment, const std::size_t size) noexcept;
```

```
void delete(void* ptr) noexcept;
void delete(void* ptr, size_t size) noexcept;
void delete(void* ptr, std::align_val alignment) noexcept;
void delete(void* ptr, size_t size, std::align_val alignment) noexcept;
void delete(void* ptr, size_t size, const std::size_t size) noexcept;
void delete(void* ptr, std::align_val alignment, const std::size_t size) noexcept;
```

```
void* operator new(size_t size);
void* operator new(size_t size, std::align_val alignment);
void* operator new(size_t size, const std::size_t size) noexcept;
void* operator new(size_t size, std::align_val alignment, 
-const std::size_t size) noexcept;
```

```
void delete(void* ptr) noexcept;
void delete(void* ptr, size_t size) noexcept;
void delete(void* ptr, std::align_val alignment) noexcept;
void delete(void* ptr, size_t size, std::align_val alignment) noexcept;
void delete(void* ptr, const std::size_t size) noexcept;
void delete(void* ptr, std::align_val alignment, const std::size_t size) noexcept;
```

```
void* operator new(size_t size, void* ptr) noexcept;
void* operator new(size_t size, void* ptr) noexcept;
void delete(void* ptr, size_t size) noexcept;
void delete(void* ptr, void* ptr) noexcept;
```

# 21.6.2 Storage allocation and deallocation

1 Except where otherwise specified, the provisions of 6.7.4 apply to the library versions of operator new and operator delete. If the value of an argument size passed to any of these functions is not a valid alignment, the behavior is undefined.

# 21.6.2.1 Single-object (std::size_t size)

```
void* operator new(size_t size);
void* operator new(size_t size, std::align_val alignment);
```

© ISO/IEC 2017 - All rights reserved

493