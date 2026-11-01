
```cpp
int modifying_factor;

void prepare_new_environment_data(int input)
{
    int result = 0;
    /* ... prepare the new environment data using input */
    modifying_factor = result;
}

int f2(int num)
{
    int calculation = 0;
    /* ... perform f2-relevant calculations */
    return calculation * modifying_factor;
}
```

```cpp
/* elevation.h */
void change_height(int new_height);
int height();

/* elevation.c */
int height_ = 0;

void change_height(int new_height)
{
    height_ = new_height;
}

int height()
{
    return height_;
}
```

```cpp
struct house
{
    int plot_size[2];
    int floor_area;
    int floor_count;
    int room_count;
    int window_count;
};
```

```cpp
class house
{
public:
    int get_plot_x() const;
    int get_plot_y() const;
    int get_floor_area() const;
    int get_floor_count() const;
    int get_room_count() const;
    int get_window_count() const;

    void set_plot_size(int x, int y);
    void set_floor_area(int area);
    void set_floor_count(int floor_count);
    void set_room_count(int room_count);
    void set_window_count(int window_count);

private:
    int plot_size[2];
    int floor_area;
    int floor_count;
    int room_count;
    int window_count;
};
```

```cpp
void house::set_floor_area(int area)
{
    floor_area = area;
    assert(floor_area < plot_size[0] * plot_size[1]);
}
```

```cpp
class account
{
public:
    void set_balance(int);
    int get_balance() const;

private:
    int balance;
};
```

```cpp
class account
{
public:
    void deposit(int);
    void withdraw(int);
    int balance() const;

private:
    int balance_;
};
```

```cpp
class point
{
public:
    void set_x(float new_x) {
        x_ = new_x; }
    void set_y(float new_y) {
        y_ = new_y; }
    float get_x() const {
        return x_; }
    float get_y() const {
        return y_; }

private:
    float x_;
    float y_;
};
```

```cpp
class team
{
public:
    void add_player(std::string name) {
        if (players_.size() < 11) players_.push_back(name); }
    std::vector<string> get_players() const {
        return players_; }

private:
    std::vector<string> players_;
};
```

## 空气的有趣性质

### 关于气体液化的新观察

### 某些气体在远高于其临界温度的温度下的冷凝

气体的临界温度是指，超过该温度后，无论施加多大压力，仅靠压力都无法使其液化。在低于这一临界点的温度下，气体可以被冷凝，并且如果压力足够高，就会变成液体。这里所探讨其性质的气体，是指在普通条件下仍保持气态的气体，因此通常被称为不沸腾气体。

下表列出了当压力降至极低点时，这些气体中较重要的几种停止沸腾的温度。可以注意到，这些温度通常远低于这些物质的普通沸点，并且常常远高于相应气体的临界温度。

**表 I.**

**不沸腾气体的温度。**

| 气体 | 温度 |
| --- | --- |
| 二氧化碳 | 31° C. |
| 氧气 | -118.8° C. |
| 氮气 | -146.9° C. |
| 氢气 | -240.3° C. |
| 氦气 | -267.9° C. |

这些数字表明，所谓的永久气体在常温下离冷凝状态有多么遥远。然而，开篇标题中描述的最新观察表明，在适当条件下，某些气体可以在远高于其临界温度的温度下冷凝。这一显著结果具有重大的理论意义，有望为我们对气态物质物理性质的认识带来许多启发。

关于气体在真空中的冷凝，已经开展了进一步的实验。人们相信，这些实验不仅将解释已经观察到的事实，还将引导我们发现空气及构成大气的其他气体的许多新性质。

```cpp
template <class T> int fn(T a, int b); // Partial specialization
template <> int fn(float a, int b); // Explicit specialization
template class cl<int>; // Explicit instantiation
```

```cpp
namespace cg30 {
... // more declarations
}
```

```cpp
// Warn if the return value is discarded rather than assigned
[[nodiscard]] int fn(int a);
```

```asm
asm {
    push rsi
    push rdi
    sub rsp, 184
}
```

```cpp
namespace rv = std::ranges::views;
```

```cpp
using std::string; // Now you no longer need to type the
// std:: prefix in this block for string
```

```cpp
using namespace std; // Never do this at global namespace scope. Ever.
// Ever, ever. Not with ANY namespace.
```

```cpp
static_assert(sizeof(int) == 4); // Assert that an int is four bytes big
```

```cpp
enum struct country : short;
```

```cpp
using flump_fn_ptr = void(*)(int);

struct flumper {
    flump_fn_ptr flump;
    ...
};

void flump_fn(int);

void fn()
{
    flumper fl { flump_fn };
    fl.flump(7);
}
```

```cpp
char *p, c, a[7], *pp[7], **aa[10];
```

```cpp
char *p; char c; char a[7]; char *pp[7]; char **aa[10];
```

```cpp
int a[2] = {1, 2};
auto [x, y] = a;  // x = a[0], y = a[1]
```

```cpp
std::unordered_map<std::string, int> dictionary;
auto [it, flag] = dictionary.insert({"one", 1});
    // it points to the element
    // flag signals whether the insertion was successful
```

```cpp
struct s {
    int a;
    float b;
};

s make_s();

auto [sa, sb] = make_s();  // sa is an int
                          // sb is a float
```

```cpp
std::unordered_map<std::string, int> dictionary;
auto [it,    // it points to the element
    flag]   // flag signals whether the insertion was successful
    = dictionary.insert({"one", 1});
```

```cpp
int display(int ID)
{
    auto h = get_handle_to_resource(ID);
    if (h == 0) {
        return 0;
    }
    auto j = manipulate_resource(h);
    if (j < 0) {
        release_handle(h);
        return 0;
    }
    auto k = supply_resource_to_system(h, j);
    if (k < 0) {
        return 0; /* forgot to release handle */
    }
    display_resource(h);
    release_handle(h);
    return 1;
}
```

```cpp
int display(int ID)
{
    auto result = 0;
    auto h = get_handle_to_resource(ID);
    if (h != 0) {
        auto j = manipulate_resource(h);
        if (j >= 0) {
            auto k = supply_resource_to_system(h, j);
            if (k >= 0) {
                display_resource(h);
                result = 1;
            }
        }
    }
    release_handle(h);
    return result;
}
```

```cpp
int display(int ID)
{
    struct resource {
        resource(int h_) : h(h_) {}
        ~resource() { release_handle(h); }
        operator int() { return h; }

        private:
            int h;
    };

    resource r(get_handle_to_resource(ID));
    if (r == 0) {
        return 0;
    }
    auto j = manipulate_resource(r);
    if (j < 0) {
        return 0;
    }
    auto k = supply_resource_to_system(r, j);
    if (k < 0) {
        return 0;
    }
    display_resource(r);
    return 1;
}
```

```cpp
void display(int ID)
{
    struct resource {
        resource(int h_) : h(h_) {}
        ~resource() { release_handle(h); }
        operator int() { return h; }

        private:
            int h;
    };

    resource r(get_handle_to_resource(ID));
    auto j = manipulate_resource(r);
    supply_resource_to_system(r, j);
    display_resource(r);
}
```

```cpp
template <class T, class release_fn>
struct RAII
{
    RAII(T t_) : t(t_) {}
    ~RAII() { release_fn r; r(t); }
    operator T() { return t; }

private:
    T t;
};
```
