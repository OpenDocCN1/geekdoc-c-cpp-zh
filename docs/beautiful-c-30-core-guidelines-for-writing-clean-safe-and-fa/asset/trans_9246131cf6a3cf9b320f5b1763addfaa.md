
```cpp
void accumulate_mst(std::vector<my_special_type>& vec_mst,
                    std::vector<int> const& source) {
    auto source_it = source.begin();
    while (source_it != source.end()) {
        auto s_it = source_it++;
        vec_mst.emplace_back(*s_it, *s_it);
    }
}
```

```cpp
void qsort(void* base, size_t num, size_t size,
int(*comp)(const void*, const void*));
```

```cpp
template <typename T>
void sort(T* base, size_t num, size_t size,
    int(*comp)(const T*, const T*));
```

```cpp
template <typename T>
void sort(T* base, size_t num, int(*comp)(const T*, const T*));
```

```cpp
template <typename T, typename F>
void sort(T* base, size_t num, F fn);
```

```cpp
template <typename InIt, typename F>
void sort(InIt first, InIt last, F fn);
```

```cpp
template <typename R, typename F>
void sort(R&& r, F fn);
```

```cpp
template <std::ranges::random_access_range R, typename F>
void sort(R&&, F fn);
```

```cpp
template <std::ranges::random_access_range R,
    typename Comp = std::ranges::less, typename Proj = std::identity>
requires std::sortable<std::ranges::iterator_t<R>, Comp, Proj>
constexpr std::ranges::borrowed_iterator_t<R>
sort(R&& r, Comp comp={}, Proj proj={});
```

```cpp
#include <vector>
int main() {
    auto vi = new std::vector<int>;
}
```

```cpp
#include <vector>
#include <memory>
int main() {
    auto vi = std::unique_ptr<std::vector<int>>(new std::vector<int>);
}
```

```cpp
#include <vector>
#include <memory>
int main() {
    auto vi = std::make_unique<std::vector<int>>();
}
```

```cpp
#include <cstdio>
int main() {
    std::fopen("output.txt", "r");
}
```

```cpp
#include <cstdio>
int main() {
    auto file = std::fopen("output.txt", "r");
}
```

```cpp
#include <fstream>
int main()
{
    auto file = std::fstream{ "output.txt" };
}
```

```cpp
#include <cstdio>
class FILE_holder {
public:
    FILE_holder(std::FILE* f) : m_f(f) {}
    ~FILE_holder() { std::fclose(m_f); }
    operator std::FILE*() { return m_f; }

private:
    std::FILE* m_f;
};

int main()
{
    auto file = FILE_holder(std::fopen("output.txt", "r"));
}
```

```cpp
template<class T>
struct default_delete {
    constexpr default_delete() noexcept = default;
    template<class U>
    default_delete(const default_delete<U>&) noexcept {}
    void operator()(T* p) const { delete p; }
};
```

```cpp
#include <memory>
#include <cstdio>

template <>
struct std::default_delete<std::FILE> {
  void operator()(std::FILE* f) { std::fclose(f); }
};

int main()
{
  auto file = std::unique_ptr<std::FILE>(std::fopen("output.txt", "r"));
}
```

```cpp
int open_database(const char*);
void close_database(int);

int main()
{
    auto db = open_database("//network/customer.db");
}
```

```cpp
#include <memory>

int open_database(const char*);
void close_database(int);

struct DATABASE_PROXY {
    DATABASE_PROXY(int db_) : db(db_) {}
    operator int() { return db; }
    int db;
};

template <>
struct std::default_delete<DATABASE_PROXY> {
    void operator()(DATABASE_PROXY* p) { close_database(*p); }
};
int main()
{
    auto db = std::unique_ptr<DATABASE_PROXY>
        (new DATABASE_PROXY(open_database("//network/customer.db")));
}
```

```cpp
template <class EF> class scope_exit;
template <class EF> class scope_fail;
template <class EF> class scope_success;
template <class R, class D> class unique_resource;
```

```cpp
void grow(vector<int>& v) {
    std::experimental::scope_success guard([]{
    std::cout << "Good!" << std::endl; });
    v.resize(1024);
}
```

```cpp
#include <experimental/scope>
#include <cstdio>

int main()
{
    using std::experimental::unique_resource;
    auto file = unique_resource(
        std::fopen("output.txt", "r"),
        [](auto fp){ std::fclose(fp); });
}
```

```cpp
#include <experimental/scope>
#include <cstdio>

int main()
{
    auto file = std::experimental::make_unique_resource_checked(
        std::fopen("potentially_nonexistent_file.txt", "r"),
        nullptr,
        [](auto fptr){ std::fclose(fptr); });
}
```
