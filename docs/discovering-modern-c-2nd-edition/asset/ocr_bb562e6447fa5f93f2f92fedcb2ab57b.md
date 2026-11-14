```
template <typename state_type>
void resize(const state_type& in, state_type& out) {
// standard implementation works for containers
using std::size;
out.resize(size(in));
}

// specialization for std::array
template <typename T, std::size_t N>
void resize(const std::array<T, N>& , std::array<T,N>& ) {
/* arrays don't need resizing */
}

template < ... >
class runge_kutta4 {
// ...
template <typename Sys>
void do_step(Sys sys, state_type& x,
time_type t, time_type dt)
{
adjust_size(x);
// ...
}
}

void adjust_size(const state_type& x) {
resize(x, x_tmp);
resize(x, k1);
resize(x, k2);
resize(x, k3);
resize(x, k4);
}
};
```