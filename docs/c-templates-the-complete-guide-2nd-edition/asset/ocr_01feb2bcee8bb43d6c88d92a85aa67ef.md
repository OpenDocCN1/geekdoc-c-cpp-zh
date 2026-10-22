```
is_const<int [3]>::value      // false
is_const<int const[3]>::value  // true
is_const<int []>::value        // false
is_const<int const[]>::value   // true
```