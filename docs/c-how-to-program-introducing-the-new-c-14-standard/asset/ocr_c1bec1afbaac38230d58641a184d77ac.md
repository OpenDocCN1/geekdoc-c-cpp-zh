# `vector` *Member Functions* `front` and `back`

Lines 20–21 use functions `front` and `back` (available for most *sequence containers*) to determine the `vector`’s first and last elements, respectively. Notice the difference between functions `front` and `begin`. Function `front` returns a reference to the first element in the `vector`, while function `begin` returns a *random-access iterator* pointing to the first element in the `vector`. Also notice the difference between functions `back` and `end`. Function `back` returns a reference to the `vector`’s last element, whereas function `end` returns a *random access iterator* pointing to the location *after* the last element.

![](bbox=[0.118, 0.54, 0.191, 0.598])

# Common Programming Error 15.2

> *The results of* `front` *and* `back` *are undefined when called on an empty* `vector`.