```
var c = new Circle(42);
Circle copy; // Uninitialized !!!
...
if (copy == // only assign to copy if it is uninitialized, but what goes here?)
{
    copy = c; // copy and c refer to the same object
    ...
}
```