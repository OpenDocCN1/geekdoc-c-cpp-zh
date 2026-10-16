
for (int i=0; i<1000; ++i)

v.push_back(randint(1000)); // §40.7

constexpr int n = 30;

nth_element(v.begin(), v.begin()+n, v.end());

cout << "nth: " << v[n] << '\n';

for (int i=0; i<n; ++i)

cout << v[i] << ' ';

```

这将产生：

```

nth: 24

10 8 15 19 21 15 8 7 6 17 21 2 18 8 1 9 3 21 20 18 10 7 3 3 8 11 11 22 22 23

```

nth_element() 与 partial_sort() 的不同之处在于，n 之前的元素不一定有序，只是都小于第 n 个元素。在该示例中将 nth_element 替换为 partial_sort（并使用相同的随机数生成器种子以获得相同的序列），我得到：

```

nth: 995

1233367788889101011115151718181920212121222223

```

nth_element() 算法对于需要查找中位数、百分位数等的人——例如经济学家、社会学家和教师——特别有用。

对 C 风格字符串进行排序需要显式的排序准则。原因在于 C 风格字符串只是带有一组使用约定的指针，因此指针上的 < 比较的是机器地址，而不是字符序列。例如：

```

vector<string> vs = {"Helsinki","Copenhagen","Oslo","Stockholm"};

vector<char*> vcs = {"Helsinki","Copenhagen","Oslo","Stockholm"};

void use() {

sort(vs); // Ihave defined a range version of sort() sort(vcs);

for (auto& x : vs)

cout << x << ' '

cout << '\n';

for (auto& x : vcs)

```

```

```cpp
cout << x << " ";
```

```

这会打印：

Copenhagen Helsinki Stockholm Oslo  
Helsinki Copenhagen Oslo Stockholm

我们可能天真地期望这两个 `vector` 容器产生相同的输出。然而，要按字符串值而不是地址对 C 风格字符串排序，我们需要一个合适的排序谓词。例如：

```

```cpp
sort(vcs, [](const char * p, const char* q){ return strcmp(p,q)<0; });
```

```

标准库函数 `strcmp()` 在 §43.4 中描述。  
请注意，我不需要提供 `==` 来对 C 风格字符串排序。为简化用户界面，标准库使用 `!(x<y)||y<x` 而不是 `x==y` 来比较元素（§31.2.2.2）。

# 32.6.1 二分查找

**二分查找 (§iso.25.4.3)**  
**p=lower_bound(b,e,v)** p 指向 **[b:e)** 中 **v** 的首次出现位置  
**p=lower_bound(b,e,v,f)** p 指向 **[b:e)** 中 **v** 的首次出现位置，使用 **f** 进行比较  
**p=upper_bound(b,e,v)** p 指向 **[b:e)** 中第一个大于 **v** 的值  
**p=upper_bound(b,e,v,f)** p 指向 **[b:e)** 中第一个大于 **v** 的值，使用 **f** 进行比较  
**binary_search(b,e,v)** **v** 是否在已排序序列 **[b:e)** 中？  
**binary_search(b,e,v,f)** 使用 **f** 进行比较，**v** 是否在已排序序列 **[b:e)** 中？  
**pair(p1,p2)=equal_range(b,e,v)** [p1,p2) 是 **[b:e)** 中值为 **v** 的子序列；基本上是对 **v** 进行的二分查找  
**pair(p1,p2)=equal_range(b,e,v,f)** [p1,p2) 是 **[b:e)** 中值为 **v** 的子序列，使用 **f** 进行比较；基本上是对 **v** 进行的二分查找

诸如 `find()`（§32.4）之类的顺序搜索对于大型序列来说效率极低，但这是我们在不进行排序或哈希（§31.4.3.2）的情况下所能做到的最好方法。然而，一旦序列已排序，我们就可以使用二分查找来确定一个值是否在序列中。例如：

```

```cpp
void f(vector<int>& c) {
if (binary_search(c.begin(),c.end(),7)) { // is 7 in c?

// ...
}
// ...
}
```

```

**binary_search()** 返回一个 `bool`，指示某个值是否存在。与 `find()` 一样，我们通常还想知道该值的元素在序列中的位置。然而，序列中可能有许多具有给定值的元素，我们常常需要找到第一个或所有这样的元素。因此，提供了用于查找相等元素范围的算法 `equal_range()`，以及用于查找该范围的 `lower_bound()` 和 `upper_bound()` 的算法。这些算法对应于 multimap 上的操作（§31.4.3）。我们可以将 `lower_bound()` 视为有序序列的快速 `find()` 和 `find_if()`。例如：

```

void g(vector<int>& c)

{

  auto p = find(c.begin(),c.end(),7); // probably slow: O(N); c needn’t be sorted

  auto q = lower_bound(c.begin(),c.end(),7); // probably fast: O(log(N)); c must be sorted // …

}

```

如果 `lower_bound(first,last,k)` 没有找到 `k`，它会返回一个指向第一个键大于 `k` 的元素的迭代器；如果不存在这样的元素，则返回 `last`。这种报告失败的方式也用于 `upper_bound()` 和 `equal_range()`。这意味着我们可以使用这些算法来确定在有序序列中插入新元素的位置，从而使序列保持有序：只需在返回的 pair 的第二个迭代器之前插入即可。

奇怪的是，二分查找算法并不需要随机访问迭代器：前向迭代器就足够了。

# 32.6.2 merge()

`merge` 算法将两个有序（已排序）序列合并为一个：

**merge 家族 (siso.25.4.4)**

| 函数 | 描述 |
|---|---|
| `p=merge(b,e,b2,e2,out)` | 将两个有序序列 `[b2:e2)` 和 `[b:e)` 合并到 `[out:p)` |
| `p=merge(b,e,b2,e2,out,f)` | 将两个有序序列 `[b2:e2)` 和 `[b:e)` 合并到 `[out,out+p)`，使用 `f` 进行比较 |
| `inplace_merge(b,m,e)` | 将两个有序子序列 `[b:m)` 和 `[m:e)` 合并为有序序列 `[b:e)` |
| `inplace_merge(b,m,e,f)` | 将两个有序子序列 `[b:m)` 和 `[m:e)` 合并为有序序列 `[b:e)`，使用 `f` 进行比较 |

`merge()` 算法可以接受不同类型的序列和不同类型的元素。例如：

```

vector<int> v {3,1,4,2};

list<double> lst {0.5,1.5,2,2.5}; // lst is in order

sort(v.begin(),v.end()); // put v in order

vector<double> v2;

merge(v.begin(),v.end(),lst.begin(),lst.end(),back_inserter(v2)); // merge v and lst into v2

for (double x : v2)

cout << x << “, “;

```

关于插入迭代器，请参阅 §33.2.2。输出为：


0.5, 1, 1.5, 2, 2, 2.5, 3, 4,

# 32.6.3 集合算法

这些算法将序列视为元素的集合，并提供基本的集合操作。输入序列应当已经排序，输出序列也会保持排序。

集合算法（§iso.25.4.5）

```

includes(b,e ,b2,e2) includes(b,e ,b2,e2,f)

p=set_union(b,e,b2,e2,out)

p=set_union(b,e,b2,e2,out,f)

p=set_intersection(b,e ,b2,e2,out)

p=set_intersection(b,e ,b2,e2,out,f)

p=set_difference(b,e ,b2,e2,out)

p=set_difference(b,e ,b2,e2,out,f)

p=set_symmetric_difference(b,e ,b2,e2,out)

p=set_symmetric_difference(b,e ,b2,e2,out,f)

```

`[b:e)` 中的所有元素是否也都在 `[b2:e2)` 中？使用 `f` 进行比较时，`[b:e)` 中的所有元素是否也都在 `[b2:e2)` 中？
构造一个排序后的序列 `[out:p)`，其中包含位于 `[b:e)` 或 `[b2:e2)` 中的元素。
构造一个排序后的序列 `[out:p)`，其中包含位于 `[b:e)` 或 `[b2:e2)` 中的元素，并使用 `f` 进行比较。
构造一个排序后的序列 `[out:p)`，其中包含同时位于 `[b:e)` 和 `[b2:e2)` 中的元素。
构造一个排序后的序列 `[out:p)`，其中包含同时位于 `[b:e)` 和 `[b2:e2)` 中的元素，并使用 `f` 进行比较。
构造一个排序后的序列 `[out:p)`，其中包含位于 `[b:e)` 但不位于 `[b2:e2)` 中的元素。
构造一个排序后的序列 `[out:p)`，其中包含位于 `[b:e)` 但不位于 `[b2:e2)` 中的元素，并使用 `f` 进行比较。
构造一个排序后的序列 `[out:p)`，其中包含位于 `[b:e)` 或 `[b2:e2)` 但不同时位于两者中的元素。
构造一个排序后的序列 `[out:p)`，其中包含位于 `[b:e)` 或 `[b2:e2)` 但不同时位于两者中的元素，并使用 `f` 进行比较。

例如：

```

string s1 = "qwertyasdfgzxcvb";

string s2 = "poiuyasdfg/.,mnb";

sort(s1.begin(),s1.end()); // 集合算法要求序列已排序

sort(s2.begin(),s2.end());

string s3(s1.size()+s2.size(), ' *'); // 为可能产生的最大结果预留足够空间

cout << s3 << '\n';

auto up = set_union(s1.begin(),s1.end(),s2.begin(),s2.end(),s3.begin());

cout << s3 << '\n';

for (auto p = s3.begin(); p!=up; ++p)

cout << *p;

cout << '\n';

```

```

s3.assign(s1.size()+s2.size(),'+');

up = set_difference(s1.begin(),s1.end(),s2.begin(),s2.end(),s3.begin()); cout << s3 << '\n';

for (auto p = s3.begin(); p!=up; ++p)

cout << *p;

cout << '\n';

```

这个小测试会产生：

```

* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * ,./abcdefghijklmnopqrstuvwxyz

ceqrtvwxz+++++++++++++++++++++++++++++ ceqrtvwxz

```

# 32.6.4 堆

堆是一种紧凑的数据结构，它将值最大的元素放在最前面。可以将堆看作二叉树的一种表示形式。堆算法允许程序员将一个随机访问序列作为堆来处理：

```

make_heap(b,e) make_heap(b,e,f) push_heap(b,e) push_heap(b,e,f) pop_heap(b,e)

pop_heap(b,e,f) sort_heap(b,e) sort_heap(b,e,f) is_heap(b,e)

is_heap(b,e,f)

p=is_heap_until(b,e) p is the largest p such that [b:p) is a heap

p=is_heap_until(b,e,f) p is the largest p such that [b:p) is a heap, using f for comparison

```

## 堆操作（§iso.25.4.6）

使 `[b:e)` 可以作为堆使用。
使用 `f` 进行比较，使 `[b:e)` 可以作为堆使用。
将 `*(e-1)` 添加到堆 `[b:e-1)` 中；之后 `[b:e)` 是一个堆。
使用 `f` 进行比较，将一个元素添加到堆 `[b:e-1)` 中。
从堆 `[b:e)` 中移除 `*(e-1)`；之后 `[b:e-1)` 是一个堆。
使用 `f` 进行比较，从堆 `[b:e)` 中移除元素。
对堆 `[b:e)` 进行排序。
使用 `f` 进行比较，对堆 `[b:e)` 进行排序。
`[b:e)` 是一个堆吗？
使用 `f` 进行比较，`[b:e)` 是一个堆吗？

第 32.6.4 节 堆 949

将堆 `[b:e)` 的末尾 `e` 想象成一个指针，它会因 `pop_heap()` 而递减，因 `push_heap()` 而递增。通过读取 `b`（例如 `x=*b`）可以提取最大元素，然后执行 `pop_heap()`。通过向 `e` 写入新元素（例如 `*e=x`）可以插入新元素，然后执行 `push_heap()`。例如：

```

string s = "herewego";

make_heap(s.begin(),s.end()); // rogheeew

pop_heap(s.begin(),s.end()); // rogheeew

pop_heap(s.begin(),s.end()-1); // ohgeeerv

pop_heap(s.begin(),s.end()-2); // hegeeorw

* (s.end()-3)='f';

```

```

push_heap(s.begin(),s.end()-2); // hegeefrw

*(s.end()-2)='x';

push_heap(s.begin(),s.end()-1); // xeheefge

*(s.end()-1)='y';

push_heap(s.begin(),s.end()); // yxheefge

sort_heap(s.begin(),s.end()); // eee fghxy

reverse(s.begin(),s.end()); // yxhgfeee

```

理解 `s` 发生变化的方式是：用户只读取 `s[0]`，并且只写入 `s[x]`，其中 `x` 是当前堆末尾的索引。堆通过将元素（始终是 `s[0]`）与 `s[x]` 交换来移除元素。

堆的作用是快速添加元素，并快速访问值最大的元素。堆的主要用途是实现优先队列。

# 32.6.5 lexicographical_compare()

字典序比较是我们在字典中排列单词时所使用的规则。

字典序比较（§iso.25.4.8）

```

lexicographical_compare(b,e ,b2,e2) Is [b:e)<[b2:e2)?

lexicographical_compare(b,e ,b2,e2,f) Is [b:e)<[b2:e2), using f for element comparison?

We might implement lexicographical_compare(b,e ,b2,e2) like this:

```

```

template<class In, class In2>

bool lexicographical_compare(In first, In last, In2 first2, In2 last2)

{

for (; first!=last && first2!=last2; ++first,++last) {

if (*first<*first2)

return true; // [first:last)<[first2:last2)

if ( *first2<*first)

return false; // [first2:last2)<[first:last)

}

return first==last && first2!=last2; // [first:last)<[first2:last2) if [first:last) is shorter

}

```

也就是说，字符串会按照字符序列进行比较。例如：

```

string n1 {"10000"}; string n2 {"999"};
