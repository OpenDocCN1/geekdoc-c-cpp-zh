```
```cpp
cout << "\\n";
for (i=0;i<d.size();i++)
cout << d[i] << "\\t";
cout << "\\n";
return 0;
}
```
```

+   (a) a a
+   
+       b b b
+   
+   (b) b b
+   
+       a a a
+   
+   (c) 97 97
+   
+       98 98 98
+   
+   (d) Compilation error

**Answer: (a)** is the correct answer. Since the data type is correctly associated with the vector, we have correct answer at this attempt.

# **12.** Predict the output of the following code snippet? (L3)

```
```cpp
# include <iostream>
# include <queue>
using namespace std;
int main()
{
    queue <int> q;
    int i;
    for (i=1; i<=5; i++)
    q.push(i);
    while (!q.empty())
    {
        cout <<q.front() <<" ";
        q.pop();
    }
    cout <<"\\n";
    return 0;
}
```
```

+   (a) Compilation error
+   (b) 1 2 3 4 5
+   (c) 5 4 3 2 1
+   (d) None of the above

**Answer: (b)** This code depicts the simplest way of constructing queues.

# **13.** Predict the output of the following code snippet? (L3)

```
```cpp
# include <iostream>
using namespace std;
int main()
{
    queue <int> q;
    int i;
    for (i=1; i<=5; i++)
    q.push(i);
    while (!q.empty())
    {
        cout <<q.front() <<" ";
        q.pop();
    }
    cout <<"\\n";
    return 0;
}
```
```

+   (a) Compilation error
+   (b) 1 2 3 4 5
+   (c) 5 4 3 2 1
+   (d) None of the above

**Answer: (a)** Without having the appropriate header file include <queue> the code will not be recognized properly by the compiler.