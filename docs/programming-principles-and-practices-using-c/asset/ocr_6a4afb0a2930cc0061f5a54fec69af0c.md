# **19.5.4 unique_ptr**

So, make_vec() is a useful kind of function that obeys the basic rules for good resource management in the presence of exceptions. It provides the basic guarantee – as all good functions should – when we want to recover from exception throws. Unless something nasty is done with nonlocal data in the “fill the vector with data” part, it even provides the strong guarantee. However, that try... catch code is still ugly. The solution is obvious: somehow we must use RAII; that is, we need to provide an object to hold that vector<int> so that we can delete the vector if an exception occurs. In <memory>, the standard library provides unique_ptr for that:

```
```c++
vector<int>* make_vec()  // make a filled vector
{
    unique_ptr<vector<int>> p(new vector<int>);  // allocate on free store
    // ... fill the vector with data; this may throw an exception ...
    return p.release();  // return the pointer held by p
}
```
```

A unique_ptr is an object that holds a pointer. We immediately initialize it with the pointer we got from new. We can use -> and * on a unique_ptr exactly like a built-in pointer (e.g., p->at(2) or (*p).at(2)), so we think of unique_ptr as a kind of pointer. However, the unique_ptr owns the object pointed to: when the unique_ptr is destroyed, it deletes the object it points to. That means that if an exception is thrown while the vector<int> is being filled, or if we return prematurely from make_vec, the vector<int> is properly destroyed. The p.release() extracts the contained pointer (to the vector<int>) from p so that we can return it, and it also makes p hold the nullptr so that destroying p (as is done by the return) does not destroy anything.

Using unique_ptr simplifies make_vec() immensely. Basically, it makes make_vec() as simple as the naïve but unsafe version. Importantly, having unique_ptr allows us to repeat our recommendation to look upon explicit try-blocks with suspicion; most can – as in make_vec() – be replaced by some variant of the “Resource Acquisition Is Initialization” technique.

The version of make_vec() that uses a unique_ptr is fine, except that it still returns a pointer, so that someone still has to remember to delete that pointer. Returning a unique_ptr would solve that:

```
```c++
unique_ptr<vector<int>> make_vec()         // make a filled vector
{
    unique_ptr<vector<int>> p(new vector<int>);  // allocate on free store
    // ... fill the vector with data; this may throw an exception ...
    return p;
}
```
```