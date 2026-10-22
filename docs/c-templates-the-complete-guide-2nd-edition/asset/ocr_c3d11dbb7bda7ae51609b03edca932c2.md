```
template<typename Seq>
concept Sequence = requires(Seq seq) {
    typename Seq::iterator;
    requires Iterator<typename Seq::iterator>;
    { seq.begin() } -> Seq::iterator;
    ...
};
```