# ISO/IEC 14882:2017(E)

flags | regex_constants::match_null | regex_constants::match_continuous

If the call returns the operator *this, the operator implements start and continues as if the most recent match was not a zero-length match.

If the most recent match was not a zero-length match, the operator sets flags to flags | regex_constants::match_sall and calls regex_search(start, end, *preex, flags). If the call returns false the iterator sets this to the end-of-sequence iterator. The iterator returns *this.

In all cases where the call to regex_search returns this, match.prefix().first should be equal to the previous value of match[0], and for each index in the half-open range [0, match.size()) for match[i].matched true return distance(begin, match(i)).first.

It is unspecified how the implementation makes these adjustments.

```
regex_iterator operator++(int);
```

Effects as by:

```
++(*this);
return *this;
```

# 31.12.2 Class regex_token_iterator
[re.tokiter]

+   The class regex_token_iterator is an iterator adaptor; to say it represents a new view of an existing sequence, by enumerating the occurrences of a regular expression within that sequence, and presenting one or more sub-expressions for each match. Each positioned by the iterator is a sub_match class template instance that to say it enumerates one sub-expression for each section of the character sequence splitting: that is to say it enumerates one sub-expression for each section of the character sequence within the regular expression.

+   When regex_token_iterator is used to enumerate a single sub-expression with index -1 the iterator performs field splitting; if the character sequence does not match the regular expression

+   After it is constructed, the iterator stores a value N to sequence. It also maintains a sequence list of the sub-expressions which will be enumerated. Every operator++ uses the count N is incremented; if N exceeds or equals sub.size(), the iterator increments member position and sets N to zero.

+   If the end of sequence is reached the iterator becomes equal to the end-of-sequence iterator value, the sub-expression which has been enumerated has index -1, in which case the iterator evaluates last sub-expression to the end of the input sequence being generated, provided that the last regular match would not be an empty sequence.

The default constructor constructs an end-of-sequence iterator object, which is the only legitimate iterator to be used for the end condition. an end-of-sequence iterator is not defined. For any other iterator value a const sub_match<BidirectionalIterator>& is returned. The result of operator-> on an end-of-sequence iterator is not defined. For any other iterator value a const sub_match<BidirectionalIterator>* is returned.