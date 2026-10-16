```
copy(bestsellers.begin(),bestsellers.end(),ostream_iterator<Book>{cout,"\n"});
}
```

Because the target of partial_sort_copy() must be a random-access iterator, we cannot sort directly to cout.

If the number of elements desired to be sorted by a partial_sort() is small compared to the total number of elements, these algorithms can be significally faster than a complete sort(). Then, their complexity approaches O(N) compared to sort()’s O(N*log(N)).

The nth_element() algorithm sorts only as far as is necessary to get the Nth element to its proper place with no element comparing less than the Nth element placed after it in the sequence. For example:

```
vector<int> v;
for (int i=0; i<1000; ++i)
v.push_back(randint(1000)); // §40.7

constexpr int n = 30;
nth_element(v.begin(), v.begin()+n, v.end());
cout << "nth: " << v[n] << '\n';
for (int i=0; i<n; ++i)
cout << v[i] << ' ';
```

This produces:

```
nth: 24
10 8 15 19 21 15 8 7 6 17 21 2 18 8 1 9 3 21 20 18 10 7 3 3 8 11 11 22 22 23
```

The nth_element() differs from partial_sort() in that the elements before n are not necessarily sorted, just all less than the nth element. Replacing nth_element with partial_sort in that example (and using the same seed for the random number generator to get the same sequence), I got:

```
nth: 995
1233367788889101011115151718181920212121222223
```

The nth_element() algorithm is particularly useful for people – such as economists, sociologists, and teachers – who need to look for medians, percentiles, etc.

Sorting C-style strings requires an explicit sorting criterion. The reason is that C-style strings are simply pointers with a set of conventions for their use, so < on pointers compares machine addresses rather than character sequences. For example:

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