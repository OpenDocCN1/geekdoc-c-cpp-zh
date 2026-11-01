```
<source>: In instantiation of 'const T& lesser(const T&, const T&)
    [with T = std::unordered_map<int, int>]':
<source>:14:31: required from here
<source>:6:15: error: no match for 'operator<' (operand types are
'const std::unordered_map<int, int>' and 'const std::unordered_map<int, int>')
  6 |     return t1 < t2 ? t1 : t2;
    |           ^~~~~
In file included from ...
<filename>:1149:5: note: candidate:
'template<class _IteratorL, class _IteratorR, class _Container>
  bool __gnu_cxx::operator<(
    const __gnu_cxx::__normal_iterator<_IteratorL, _Container>&,
    const __gnu_cxx::__normal_iterator<_IteratorR, _Container>&)'
1149 |   operator<(const __normal_iterator<_IteratorL, _Container>& __lhs,
    |   ^~~~~~~~
```