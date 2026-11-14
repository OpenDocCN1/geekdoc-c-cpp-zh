```
template <typename T, typename U= T>
class complex
{
    private:
    auto uncover_members() const { return std::tuple(r, i); }
    friend complex_fixture;
};
```