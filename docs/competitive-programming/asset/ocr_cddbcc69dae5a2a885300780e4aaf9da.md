```
~~~cpp
#include <iostream>
#include <stdlib.h>
#include <string.h>
using namespace std;

char S[1001]; // this naive Suffix Array cannot go beyond 1000 characters
int SA[1001], n;                              // compare suffixes
int SA_cmp(const void *a, const void *b) { return strcmp(S + *(int*)a, S + *(int*)b); }

int main() { // first approach: O(n^2 log n), only for n <= 1000
  n = strlen(gets(S));
  for (int i = 0; i < n; i++) SA[i] = i; // sort    * comparison
  qsort(SA, n, sizeof(int), SA_cmp);     // O(n log n) * O(n) = O(n^2 log n)
  for (int i = 0; i < n; i++) printf("%d %s\n", SA[i], S+SA[i]);
} // return 0;
~~~
```

When applied to string S = `acacag$`, the simple code that simply sort all suffixes with sort library will produce the correct Suffix Array = {6, 0, 2, 4, 1, 3, 5} (note that index starts from 0). However, this is barely useful except for contest problems with n ≤ 1000.

A better way to build the Suffix Array is to sort suffixes O(n log n) in increasing length. We start from suffixes with length 1, length 2, length 4, length 8, ..., up to n. As the length grows exponentially, we only need O(log n) steps. Thus the overall complexity is O(n log^2 n). With this complexity, working with strings of length n ≤ 100K - the typical programming contest range - is not a problem. The library code is shown below. For explanation, see [29, 24].

```
~~~cpp
#include <algorithm>
#include <iostream>
#include <stdlib.h>
#include <string.h>
using namespace std;
#define MAXN 200010
int RA[MAXN], SA[MAXN], LCP[MAXN], *FC, *SC, step;
char S[MAXN], Q[MAXN];

bool cmp(int a, int b) {
  if (step==-1 || FC[a]!=FC[b]) return FC[a] < FC[b];
  return FC[a+(1<<step)] < FC[b+(1<<step)];
}

void suffix_array(char *S, int n) { // O(n log^2(n))
  for (int i=0; i<n; i++) RA[i] = S[SA[i] = i];
  for (FC=RA, SC=LCP, step=-1; (1<<step)<n; step++) {
    sort(SA, SA+n, cmp);
    int cnt = 0;
    for (int i=0; i<n; i++) {
      if (i>0 && cmp(SA[i-1],SA[i])) cnt++;
      SC[SA[i]] = cnt;
    }
    if (cnt==n-1) break; // all distinct, no need to continue
    swap(FC,SC);
  }
  for (int i=0; i<n; i++) RA[SA[i]] = i;
}
~~~
```