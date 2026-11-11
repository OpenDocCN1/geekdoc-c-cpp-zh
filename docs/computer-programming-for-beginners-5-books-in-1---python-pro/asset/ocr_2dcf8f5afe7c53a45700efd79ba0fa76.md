```
    return 1;
    } else {
    return base * power(base, exponent - 1);
    }
    }
    console.log(power(2, 3));
    // → 8
```

There is one problem with this execution. It is slower compared to other looping versions. Utilizing a single loop is considered low cost than the multiple calling of functions. Although that does not make recursion an ineffective option of looping, few problems are solved with recursion easier than with the use of loops. Problems that need inspecting or processing several branches. Check this out: we begin from number 1 and continuously add 5 or multiply by 3. For instance, the number 13 can be obtained by multiplying by 3 and the addition of 5 twice, thereby we cannot attain the 15. The code is the recursive solution:

```
    function findSolution(target) {
    function find(current, history) {
    if (current == target) {
    return history;
    } else if (current > target) {
    return null;
    } else {
    return find(current + 5, `${history} + 5`) ||
    find(current * 3, `${history} * 3`);
    }
    }
    return find(1, "1");
    }
    console.log(findSolution(24));
    // → (((1 * 3) + 5) * 3)
```

The inner function find takes two arguments, the current number and a string that documents the process of attaining this number. If a solution is found, it sends back a string that displays the route to the target and if no solution is found, the returned value will be null. To achieve this, the function executes one of three actions. If your target is the current number, you can attain that target by using the current history so it is sent back. Sometimes the number is larger than the target, but you do not need to explore this option because addition and multiplication can only enlarge the number, so it is sent back as null. If you remain beneath the