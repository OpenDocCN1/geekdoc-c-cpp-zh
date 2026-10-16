# 5.3.2 Passing Arguments

Typically, a task needs data to work upon. We can easily pass data (or pointers or references to the data) as arguments. Consider:

```
void f(vector<double>& v); // function do something with v
function object: do something with v struct F { //
vector<double>& v;
F(vector<double>& vv) :v{vv} { }
void operator()(); // application operator ;§3.4.3
};
int main() {
vector<double> some_vec {1,2,3,4,5,6,7,8,9}; vector<double> vec2 {10,11,12,13,14};
thread t1 {f,some_vec}; thread t2 {F{vec2}};
// f(some_vec) executes in a separate thread // F(vec2)() executes in a separate thread
t1.join(); t2.join();
}
```

Obviously, F{vec2} saves a reference to the argument vector in F. F can now use that array and hopefully no other task accesses vec2 while F is executing. Passing vec2 by value would eliminate that risk.

The initialization with {f,some_vec} uses a thread variadic template constructor that can accept an arbitrary sequence of arguments (§28.6). The compiler checks that the first argument can be invoked given the following arguments and builds the necessary function object to pass to the thread. Thus, if F::operator()() and f() perform the same algorithm, the handling of the two tasks are roughly equivalent: in both cases, a function object is constructed for the thread to execute.

# 5.3.3 Returning Results

In the example in §5.3.2, I pass the arguments by nonconst reference. I only do that if I expect the task to modify the value of the data referred to (§7.7). That’s a somewhat sneaky, but not uncommon, way of returning a result. A less obscure technique is to pass the input data by const reference and to pass the location of a place to deposit the result as a separate argument:

```
void f(const vector<double>& v, double* res);// takeinput from v; place result in *res
class F {
public:
F(const vector<double>& vv, double* p) :v{vv}, res{p} { }
void operator()(); // place result in *res
```

```
private:
const vector<double>& v; // source of input double*res; // target for output
```