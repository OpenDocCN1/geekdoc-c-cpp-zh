In addition, L.index(x) returns the index of the first element equal to x, and L.remove(x) removes the first element equal to x. These commands raise an error when x is not in the list. Finally, the command del L[p:q] is equivalent to L[p:q] = [] , and del L[i] removes the ith element.
Contrary to what happens in several other computer languages, these functions modify in-place the list L, without creating a new list.

# ### 3.3.4 Examples of List Manipulations

The following example constructs the list of even terms and the list of odd terms of a given list. This first solution goes twice through the list, and this performs the parity tests twice:

```
```sage
sage: def fct1(L):
....:     return [filter (lambda n: n % 2 == 0, L),
....:             filter (lambda n: n % 2 == 1, L)]

sage: fct1([1..10])
[2, 4, 6, 8, 10], [1, 3, 5, 7, 9]
```
```

The second function below goes only once through the list, and constructs the two result lists element by element:

```
```sage
sage: def fct2(L):
....:     res0 = [] ; res1 = []
....:     for k in L:
....:         if k%2 == 0: res0.append(k) # or res0[len(res0):] = [k]
....:         else: res1.append(k)        # or res1[len(res1):] = [k]
....:     return [res0, res1]
```
```

This program replaces the for loop and the auxiliary variables by a recursive call and an additional parameter:

```
```sage
sage: def fct3a (L, res0, res1):
....:     if L == []: return [res0, res1]
....:     elif L[0]%2 == 0: return fct3a(L[1:], res0+[L[0]], res1)
....:     else: return fct3a (L[1:], res0, res1+[L[0]])
```
```

```
```sage
sage: def fct3 (L): return fct3a (L, [], [])
```
```

The parameters res0 and res1 contain the first element already treated, and the parameter list L has one term less at each recursive call.

The second example below extracts all maximal non-decreasing sequences of a list of numbers. Three variables are used, the first one res keeps track of all non-decreasing sequences already obtained, the start variable is the starting index of the current sub-sequence, and k is the loop index:

```
```sage
sage: def subSequences (L):
....:     if L == []: return []
....:     res = [] ; start = 0 ; k = 1
```
```