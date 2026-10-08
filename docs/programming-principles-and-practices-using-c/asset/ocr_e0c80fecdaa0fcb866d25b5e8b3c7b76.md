Many algorithms follow the usual convention of returning the end of a sequence to represent “not found.” We don't mention that for each algorithm.

# B.5.1 Nonmodifying sequence algorithms

A nonmodifying algorithm just reads the elements of a sequence; it does not rearrange the sequence and does not change the value of the elements:

**Nonmodifying sequence algorithms**

`f=i=for_each(b,e,f)`	Do `f` for each element in `[b:e)`; return `f`.
`p=find(b,e,v)`	`p` points to the first occurrence of `v` in `[b:e)`.
`p=find_if(b,e,f)`	`p` points to the first element in `[b:e)` so that `f(*p)`.
`p=find_first_of(b,e,b2,e2)`	`p` points to the first element in `[b:e)` so that `*p==*q` for some `q` in `[b2:e2)`.
`p=find_first_of(b,e,b2,e2,f)`	`p` points to the first element in `[b:e)` so that `f(*p,*q)` for some `q` in `[b2:e2)`.
`p=adjacent_find(b,e)`	`p` points to the first `p` in `[b:e)` such that `*p==*(p+1)`.
`p=adjacent_find(b,e,f)`	`p` points to the first `p` in `[b:e)` such that `f(*p,*(p+1))`.
`equal(b,e,b2)`	Do all elements of `[b:e)` and `[b2:b2+(e-b))` compare equal?
`equal(b,e,b2,f)`	Do all elements of `[b:e)` and `[b2:b2+(e-b))` compare equal using `f(*p,*q)` as the test?
`pair(p1,p2)=mismatch(b,e,b2)`	`(p1,p2)` points to the first pair of elements in `[b:e)` and `[b2:b2+(e-b))` for which `!(*p1==*p2)`.
`pair(p1,p2)=mismatch(b,e,b2,f)`	`(p1,p2)` points to the first pair of elements in `[b:e)` and `[b2:b2+(e-b))` for which `!f(*p1,*p2)`.
`p=search(b,e,b2,e2)`	`p` points to the first `*p` in `[b:e)` such that `*p` equals an element in `[b2:e2)`.
`p=search(b,e,b2,e2,f)`	`p` points to the first `*p` in `[b:e)` such that `f(*p,*q)` for an element `*q` in `[b2:e2)`.
`p=find_end(b,e,b2,e2)`	`p` points to the last `*p` in `[b:e)` such that `*p` equals an element in `[b2:e2)`.
`p=find_end( b,e,b2,e2,f)`	`p` points to the last `*p` in `[b:e)` such that `f(*p,*q)` for an element `*q` in `[b2:e2)`.