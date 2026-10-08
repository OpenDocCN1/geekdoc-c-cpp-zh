```
void f(vector<double>& v); // Il function: do something with v

struct F {
    vector<double>& v; // Il function object: do something with v
    F(vector<double> && vv) :v{vv} {}
    void operator()(); // Il application operator: \$7.3.2
};

int main()
{
    vector<double> some_vec {1, 2, 3, 4, 5, 6, 7, 8, 9};
    vector<double> vec2 {10, 11, 12, 13, 14};

    jthread t1 {f,ref(some_vec)}; // Il f(some_vec) executes in a separate thread
    jthread t2 {F(vec2)}; // Il F(vec2)() executes in a separate thread
}
```