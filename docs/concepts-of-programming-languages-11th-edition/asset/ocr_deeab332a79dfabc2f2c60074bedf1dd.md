2. Show the stack with all activation record instances, including static and dynamic chains, when execution reaches position 1 in the following skeletal program. Assume bigsub is at level 1.

```
```
function bigsub() {
    var mysum;
    function a() {
        var x;
        function b(sum) {
            var y, z;
            ...
            c(z);
            ...
        } // end of b
        ...
        b(x);
        ...
    } // end of a
    function c(plums) {
        ... <-------------------------------------1
    } // end of c
    var l;
    ...
    a();
    ...
} // end of bigsub
```
```

3. Show the stack with all activation record instances, including static and dynamic chains, when execution reaches position 1 in the following skeletal program. Assume bigsub is at level 1.

```
```
function bigsub() {
    function a(flag) {
        function b() {
            ... a(false);
            ...
        } // end of b
        ...
        if (flag)
            b();
        else c();
        ...
    } // end of a
    function c() {
        function d() {
            ... <-------------------------------------1
        } // end of d
        ...
        d();
```
```