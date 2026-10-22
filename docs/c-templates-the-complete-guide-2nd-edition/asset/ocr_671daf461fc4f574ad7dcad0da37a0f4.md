```
template<Sequence Seq>
    requires EqualityComparable<typename Seq::value_type>
typename Seq::iterator find(Seq const& seq,
                        typename Seq::value_type const& val)
{
    return std::find(seq.begin(), seq.end(), val);
}
```