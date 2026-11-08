```
```cpp
// comment to be a container so long as the value type

template<typename T>
requires IsConvertible<T, U>
operator Container<T>() const
{
};
```
```

The requires clause (discussed in Section 5.1 on page 70) describes the requirements of the template. If any of the requirements are not satisfied, the template is not considered a candidate. It is therefore a more direct expression of the idea expressed by Table 5.1, supported by the language itself.

The requires clause has additional benefits over enable_if. Constraint accumulation (described in Section 5.3.1 on page 74) provides an ordering among templates that offer only a tiny range of implementation choices, eliminating the need for tag dispatching. Additionally, a requires clause can be attached to a non-template. For example, to provide a sort() member function when the type T is comparable with <:

**Click here to view code image**

```
```cpp
template<typename T>
class Container {
public:
    requires HasLess<T>
    void sort() {
        ...
    }
};
```
```

# 20.4 CLASS SPECIALIZATION

Class template partial specializations can be used to provide alternate, specialized implementations of a class template for specific template arguments, much like we used overloading for function templates. And, like overloaded function templates, it can make sense to differentiate those partial specializations based on properties of the template arguments. Consider a generic Dictionary class template with key and value types as its template parameters. A simple but inefficient Dictionary can be implemented so long as the key type provides just an equality operator:

**Click here to view code image**

```
```cpp
template<typename Key, typename Value>
class Dictionary
{
private:
    vector<pair<Key, Value>> data;
public:
    // subscripted access to the data:
    Value& operator[](const Key& key)
    {
        // search for the element with this key:
        for (auto& element : data) {
            if (element.first == key) {
                return element.second;
            }
        }

        // there is no element with this key; add one
        data.push_back({key, Value{}});
        return data.back().second;
    }
};
```
```

If the key type supports a < operator, we can provide a more efficient implementation based on the standard library's map container. Similarly, if the key type supports hashing operations, we can provide an even more efficient implementation based on the standard library's unordered_map.

# 20.4.1 Enabling/Disabling Class Templates

The way to enable/disable different implementations of class templates is to use enabled/disabled partial specializations of class templates. To use isValid, we define templated partial specializations, we first introduce an unnamed, default template parameter to Dictionary:

**Click here to view code image**

```
```cpp
template<typename Key, typename Value, typename = void>
class Dictionary
{
    ...
};
```
```

This new template parameter serves as an anchor for enable_if, which may can be embedded in the template argument list of the partial specialization for the < as version of the Dictionary:

**Click here to view code image**

```
```cpp
template<typename Key, typename Value>
class Dictionary<Key, Value,
    typename = ...>
{
    ...
};
```
```