Nonmodifying sequence algorithms (continued)
| p=search_n(b,e,n,v) | p points to the first element of [b:e] such that each element in [p:p+n] has the value v. |
| p=search_n(b,e,n,v,f) | p points to the first element of [b:e] such that for each element *q in [p:p+n] we have f(*q,v). |
| x=count(b,e,v) | x is the number of occurrences of v in [b:e]. |
| x=count_if(b,e,v,f) | x is the number of elements in [b:e] so that f(*p,v). |

Note that nothing stops the operation passed to for_each from modifying elements; that’s considered acceptable. Passing an operation that changes the elements it examines to some other algorithm (e.g., count or ==) is not acceptable.

An example (of proper use):

```
bool odd(int x) { return x&1; }

int n_even(const vector<int>& v    // count the number of even values in v
{
    return v.size()-count_if(v.begin(),v.end(),odd);
}
```

# B.5.2 Modifying sequence algorithms

The modifying algorithms (also called mutating sequence algorithms) can (and often do) modify the elements of their argument sequences.

Modifying sequence algorithms
| p=transform(b,e,out,f) | Apply *p2=f(*p1) to every *p1 in [b:e], writing to the corresponding *p2 in [out:out+(e-b)]; p=out+(e-b). |
| p=transform(b,e,b2,out,f) | Apply *p3=f(*p1, *p2) to every element in *p1 in [b:e] and the corresponding element *p2 in [b2:b2+(e-b)), writing to *p3 in [out:out+(e-b)]; p=out+(e-b). |
| p=copy(b,e,out) | Copy [b:e] to [out:p). |
| p=copy_backward(b,e,out) | Copy [b:e] to [p:out) starting with its last element. |