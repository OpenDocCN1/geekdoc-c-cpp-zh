
# 算法

## 比较
`lexicographical_compare(beg1, end1, beg2, end2)`
`lexicographical_compare(beg1, end1, beg2, end2, comp)`

## 累加
`accumulate(beg, end, init)`
`accumulate(beg, end, init, binaryOp)`

## 内积
`inner_product(beg1, end1, beg2, end2, binop, bin2)`

## 部分和
`partial_sum(beg, end, dest)`
`partial_sum(beg, end, dest, binaryOp)`

## 相邻差分
`adjacent_difference(beg, end, dest)`
`adjacent_difference(beg, end, dest, binaryOp)`

# 分布

`uniform_distribution<IntT> u(m, n);`
`uniform_distribution<RealT> u(x, y);`

`bernoulli_distribution b(p);`

`binomial_distribution<IntT> b(t, p);`

`geometric_distribution<IntT> g(p);`

`negative_binomial_distribution<IntT> nb(k, p);`

`poisson_distribution<IntT> p(x);`

`exponential_distribution<RealT> e(lam);`

`gamma_distribution<RealT> g(a, b);`

`weibull_distribution<RealT> w(a, b);`

`extreme_value_distribution<RealT> e(a, b);`

`normal_distribution<RealT> n(m, s);`

`lognormal_distribution<RealT> ln(m, s);`

`chi_squared_distribution<RealT> c(x);`

`cauchy_distribution<RealT> c(a, b);`

`fisher_f_distribution<RealT> f(m, n);`

`student_distribution<IntT> s(n);`

`discrete_distribution<IntT> d(i, j);`

`discrete_distribution<IntT> d[il];`

`piecewise_constant_distribution<RealT> pc(b, e, w);`

`piecewise_linear_distribution<RealT> pl(b, e, w);`

# 随机引擎

`def random engine`

`linear congruential engine`

`mersenne_twister engine`

`subtract_with_carry engine`

`discard block engine`

`independent bits engine`

`shuffle_order_engine`
