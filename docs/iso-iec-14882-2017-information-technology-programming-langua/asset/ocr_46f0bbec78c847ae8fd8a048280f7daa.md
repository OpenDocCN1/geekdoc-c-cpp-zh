# ISO/IEC 14882:2017(E)

```
regex_token_iterator(BidirectionalIterator a, BidirectionalIterator b,
const regex_type& re,
const int (subbatches)[N],
const regex_constants::match_flag_type m = delete;
regex_token_iterator(const regex_token_iterator&);
regex_token_iterator& operator=(const regex_token_iterator&);
bool operator==(const regex_token_iterator const);
bool operator!=(const regex_token_iterator const);
const value_type* operator() const;
const value_type* operator->() const;
regex_token_iterator operator++();
regex_token_iterator operator++(int);
```

private:
using position_iterator = BidirectionalIterator<char, traits>;nposition_iterator position;
const value_type* result;
value_type suffix;
size_t N;
vector<int> subs;

+   7 A iterator is a regex_token_iterator object that points to a final sequence of characters at the end of the sequence. In this suffix the member holds a pointer to the data member suffix. suffix.match is true. first points to the beginning of the final sequence, and suffix.second points to the end of the final sequence.

> 8 Note: For a suffix, data member suffix.first is the same as the end of the last match found, and suffix.second is the same as the end of the target sequence end

+   9 The current match is (*position).prefix() if [subs[N]] == -1, or (*position)[subs[N]] for any other value of subs.

# 31.1.2.1 regex_token_iterator constructors [re.tokiter.constr]

```
regex_token_iterator();
```

+   1 Effects: Constructs the end-of-sequence iterator.

```
regex_token_iterator(BidirectionalIterator a, BidirectionalIterator b,
const regex_type& re,
int subbatches = 0,
const regex_constants::match_flag_type m = regex_constants::match_default;
```

```
regex_token_iterator(BidirectionalIterator a, BidirectionalIterator b,
const regex_type& re,
const vector<int>& subbatches,
const regex_constants::match_flag_type m = regex_constants::match_default;
```

```
regex_token_iterator(BidirectionalIterator a, BidirectionalIterator b,
const regex_type& re,
const initializer_list<int> subbatches,
const regex_constants::match_flag_type m = regex_constants::match_default;
```