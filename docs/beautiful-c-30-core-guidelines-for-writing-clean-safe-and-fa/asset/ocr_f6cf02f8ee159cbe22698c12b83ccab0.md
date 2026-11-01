Single pieces of functionality used to initialize objects often result in the creation of temporary state whose utility expires after the declaration of the object in question. Since the temporary state is a dependency of the object, it must be declared at the same scope. Bundling it into a lambda expression creates a local scope which can export a value.

# Eliminating state

Late declaration is even applicable to containers. Consider this function:

Click here to view code image

```
```cpp
void accumulate_mst(std::vector<my_special_type>&
vec_mst,
                    std::vector<int> const&
source) {
    auto source_it = source.begin();
    while (source_it != source.end()) {
        auto s_it = source_it++;
        my_special_type mst{*s_it, *s_it};
        vec_mst.push_back(mst);
    }
}
```
```

Within the while loop, an instance of my_special_type is constructed and pushed onto the vector. You might consider avoiding the construction entirely and push back an rvalue instance instead:

Click here to view code image

```
```cpp
void accumulate_mst(std::vector<my_special_type>&
vec_mst,
                    std::vector<int> const&
source) {
    auto source_it = source.begin();
```
```