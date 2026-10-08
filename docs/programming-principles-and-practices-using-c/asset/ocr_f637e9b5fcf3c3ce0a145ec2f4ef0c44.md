```
vector v2 = v;    // what happens here?
// ...
```

Ideally, **v2** becomes a copy of **v** (that is, **=** makes copies); that is, **v2.size() == v.size()** and **v2[i] == v[i]** for all i in the range **[0, v.size())**. Furthermore, all memory is returned to the free store upon exit from **f()**. That’s what the standard library **vector** does (of course), but it’s not what happens for our still-far-too-simple **vector**. Our task is to improve our **vector** to get it to handle such examples correctly, but first let’s figure out what our current version actually does. Exactly what does it do wrong? How? And why? Once we know that, we can probably fix the problems. More importantly, we have a chance to recognize and avoid similar problems when we see them in other contexts.

The default meaning of copying for a class is “Copy all the data members.” That often makes perfect sense. For example, we copy a **Point** by copying its coordinates. But for a pointer member, just copying the members causes problems. In particular, for the **vectors** in our example, it means that after the copy, we have **v.sz == v2.sz** and **v.elem == v2.elem** so that our **vectors** look like this:

![](bbox=[0.2, 0.44, 0.72, 0.53])

That is, **v2** doesn’t have a copy of **v**’s elements; it shares **v**’s elements. We could write

```
v.set(1,99);         // set v[1] to 99
v2.set(0,88);        // set v2[0] to 88
cout << v.get(0) << ' ' << v2.get(1);
```

The result would be the output **88 99**. That wasn’t what we wanted. Had there been no “hidden” connection between **v** and **v2**, we would have gotten the output **0 0**, because we never wrote to **v[0]** or to **v2[1]**. You could argue that the behavior we got is “interesting,” “neat!” or “sometimes useful,” but that is not what we intended or what the standard library **vector** provides. Also, what happens when we return from **f()** is an unmitigated disaster. Then, the destructors for **v** and **v2** are implicitly called; **v**’s destructor frees the storage used for the elements using

```
delete[] elem;
```

and so does **v2**’s destructor. Since **elem** points to the same memory location in both **v** and **v2**, that memory will be freed twice with likely disastrous results (§17.4.6).