The length of the array is determined by the number of values placed inside the curly braces. Example 7-3 creates and initializes three arrays of different types. Each statement illustrates a different way to perform the initialization.

# Example 7-3

```
```java
int [] anArray = {100, 200, 400, 600};
char [] grade = new char [] {'A', 'B', 'C', 'D', 'F'};
double [] depth = new double [2] {2.5, 3};
```
```

The first statement creates an array of four elements. The initial values are 100, 200, 400, and 600. Notice that the keyword new is not included here, and the type is not repeated. The second statement shows that the type of the value used for initialization must be compatible with the declaration type. Because char is the specified declaration type, all initialization values are enclosed in single quotes. Five elements are created using the grade identifier. No length specifier is required. But notice that this differs from the declaration of anArray in that the new keyword is used and the type is specified with opening and closing square brackets. The last statement creates an array with a length of two. The value 3 is assignment compatible with the double type. Figure 7-3 shows the memory contents after the initialization.

![](bbox=[0.177, 0.493, 0.903, 0.695])

Figure 7-3 — Methods of creating and initializing arrays at compile time

In Figure 7-3, the depth array is shown with a length indicator of 2, and two initial values are included in the declaration. Remember, the length indicator is not needed when you do a compile-time initialization. However, if you include the length indicator, it must match the number of values included. Otherwise, a syntax error is issued. The following example does not compile and generates an error:

```
```java
double [] waterDepth = new double [200] {0, 3};   //Invalid
```
```