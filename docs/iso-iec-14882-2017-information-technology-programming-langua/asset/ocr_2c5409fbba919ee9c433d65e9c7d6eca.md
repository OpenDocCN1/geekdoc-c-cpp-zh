# ISO/IEC 14882:2017(E)

```
template<class RealType = double>
class chi_squared_distribution {
public:
  // types
  using result_type = RealType;
  using param_type = unspecified;

  // constructor and reset functions
  explicit chi_squared_distribution(RealType n = 1);
  explicit chi_squared_distribution(const param_type& param);
  void reset();

  // generating functions
  template<class URB>
  result_type operator()(URB& g);
  template<class URB>
  result_type operator()(URB& g, const param_type& param);

  // property functions
  RealType n() const;
  param_type param() const;
  void param(const param_type&);
  RealType min() const;
  RealType max() const;
};

explicit chi_squared_distribution(RealType n = 1);
```

+   2 Requires: 0 < n.

+   3 Effects: Constructs a chi_squared_distribution object; n corresponds to the parameter of the distribution.

RealType n() const;

+   4 Returns: The value of n with which the object was constructed.

+   1 A cauchy_distribution produces random numbers x according to the probability density

![](bbox=[0.33, 0.626, 0.653, 0.673])

```
template<class RealType = double>
class cauchy_distribution {
public:
  // types
  using result_type = RealType;
  using param_type = unspecified;

  // constructor and reset functions
  explicit cauchy_distribution(RealType a = 0.0, RealType b = 1.0);
  explicit cauchy_distribution(const param_type& param);
  void reset();
```