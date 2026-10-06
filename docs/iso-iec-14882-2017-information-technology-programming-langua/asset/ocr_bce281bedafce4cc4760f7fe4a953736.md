# ISO/IEC 14882:2017(E)

6 It is impossible to store things into regex_token_iterators. Two end-of-sequence iterators are always equal. An end-of-sequence iterator is not equal to a non-end-of-sequence iterator. Two non-end-of-sequence iterators are equal when they are constructed from the same arguments.

```
namespace std {
    template <class BirectionalIterator,
        class charT = typename iterator_traits<BirectionalIterator>::value_type,
        class traits = regex_traits<charT>>
    class regex_token_iterator {
public:
        using reg_type = regex<charT, Traits>;
        using iterator_category = forward_iterator_tag;
        using value_type = sub_match<BirectionalIterator>;
        using difference = ptrdiff_t;
        using pointer = const value_type*;
        using reference = const value_type&;

        regex_token_iterator(BirectionalIterator a, BirectionalIterator b,
            const regex& re,
            int match = 0,
            regex_constants::match_flag_type m =
            regex_constants::match_default)
        regex_token_iterator(BirectionalIterator a, BirectionalIterator b,
            const regex& re,
            const vector<int>& submatches,
            regex_constants::match_flag_type m =
            regex_constants::match_default);
        regex_token_iterator(BirectionalIterator a, BirectionalIterator b,
            const regex& re,
            initializer_list<int> submatches,
            regex_constants::match_flag_type m =
            regex_constants::match_default);

template <size_t N>
    regex_token_iterator(BirectionalIterator a, BirectionalIterator b,
        const regex& re,
        const int (&submatches)[N],
        regex_constants::match_flag_type m =
        regex_constants::match_default);
    regex_token_iterator(BirectionalIterator a, BirectionalIterator b,
        const regex& re,
        int match = 0,
        regex_constants::match_flag_type m =
        regex_constants::match_default = delete);
    regex_token_iterator(BirectionalIterator a, BirectionalIterator b,
        const regex& re,
        const vector<int>& submatches,
        regex_constants::match_flag_type m =
        regex_constants::match_default = delete);
    regex_token_iterator(BirectionalIterator a, BirectionalIterator b,
        const regex& re,
        initializer_list<int> submatches,
        regex_constants::match_flag_type m =
        regex_constants::match_default = delete);

    template <size_t N>
```