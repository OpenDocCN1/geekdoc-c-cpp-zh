```
```cpp
template <typename T>
class Stack {
private:
    T items[100];
    int top;
public:
    // Class methods here
};
```
```

# **Type-Independent Algorithms:**

Templates facilitate the creation of algorithms and data structures that are not tied to specific data types. For instance, a sorting algorithm implemented as a function template can sort arrays of various data types without modification.

```
```cpp
template <typename T>
void bubbleSort(T arr[], int size) {
    // Sorting logic
}
```
```

# **Namespaces:**

# **Introduction and Purpose:**

Namespaces are a tool to circumvent naming conflicts and organize code. They provide a means to group related code under a common namespace,