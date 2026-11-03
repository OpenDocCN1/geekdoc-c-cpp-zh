```
16 {

16 { 16 { 16 { 16 {

16 {

16 { 16 { 16 {

16 {

16 {

16 {
```

With the *static* keyword in place, the program is now able to retain the array's content when the function finishes its execution. The function remains static. In other words, it remains unchanged. Save, build and run this code. The *encrypt* function only returns the memory address/location of the string. The other characters still reside in memory and are referenced by the *printf* function. Remember that all of this will only work if you ensure that the returned string is

Do note, however, that this particular rule isn't applicable to single values. C language functions are designed to give back single values, which also includes pointers. For other arrays, strings, or any kind of variable within a function, you have to make sure that they are static. Or else the value isn't retained as soon as the function finishes executing.