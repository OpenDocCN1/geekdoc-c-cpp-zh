# 8 • Pointers 207

```
void make_rand(void (*ptr) int evt, int num)
{
    int i, cnt;

    cnt = 0;
    while (1) {
        i = rand();
        cnt++;
        if (i >= 1000 && i <= 2000) {
            (*ptr)(cnt, i);
            return;
        }
    }
}
```

```
void handle_event(int evt, int num)
{
    std::cout << "Times:" << evt << " Num:" << num << '\n';
}
```

At first, the main program (e.g., part A) calls make_rand(e.g., evt, part B), which takes parameter a pointer to a function which accepts two integer parameters and returns nothing. Notice, that we write the name of handle_event(). When the name of a function is not followed by parentheses, the compiler uses a pointer to this function; it is careful not to call the function. To make sure you understand the difference, here is an example with two functions a and b:

```
a(b); // The address of b is passed to a.
a(b()); // b is first called, then the return value of b is passed to a.
```

make_rand() generates random integers, once an integer within [1000, 2000] is generated, it uses the pointer to callback handle_event() and passes as arguments how many numbers were generated and the number in the specified interval. This example has no practical value; I just wanted to show you an implementation example of the callback mechanism. Also, the use of a function as argument can make your function to work in a generic way. Here is an example:

```
#include <iostream> // Example 8.26
#include <vector>
using std::cout;
using std::vector;

int find_val(const vector<int>& v, int num, (*op)(int a, int b));
int max_val(int a, int b);
int min_val(int a, int b);

int main() {
    vector<int> vec(3, 8, 12, -5);

    cout << "Max:" << find_val(vec, max_val) << '\n';
    cout << "Min:" << find_val(vec, min_val) << '\n';
    return 0;
}
```