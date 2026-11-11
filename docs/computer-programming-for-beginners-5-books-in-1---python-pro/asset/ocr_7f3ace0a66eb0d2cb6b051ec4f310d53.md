```
return passed;
}
console.log(filter(SCRIPTS, script => script.living));
// → [{name: "Adlam", …}, …]
```

This function utilizes the argument called test, a function value, to cover a gap during the calculation. It determines which element to receive.

# Transforming with map

The map method changes an array by setting a function to each and every of its elements and creating a new array from the returned values. The new array consists of the same length with the input array but will map out its content to a renewed for by the function.

```
function map(array, transform) {
  let mapped = [];
  for (let element of array) {
    mapped.push(transform(element));
  }
  return mapped;
}
```

```
let rtlScripts = SCRIPTS.filter(s => s.direction == "rtl");
console.log(map(rtlScripts, s => s.name));
// → ["Adlam", "Arabic", "Imperial Aramaic", …]
```

Like forEach and filter.

# Summarizing with reduce

When you add up numbers, begin with zero and add the foreach element to the sum. The parameter to reduce are map function combination and begin a value. This function is much easier to understand than the filter and map. It is below:

```
function reduce(array, combine, begin) {
  let current = begin;
  for (let items of arrays) {
    existing = combine(existing, element);
  }
  return existing;
}
```

```
console.log(reduce([0,1, 2, 3, 4], (a, b) => a + b, 0));
// → 10
```

This function is similar to the standard array method reduce and attaches more comfort.