+   - `isLarger(a);`
+   - `else`
+   - `isLarger(b);`

```
17
18 return(o);
19 }
20
21 int max(int x, int y)
22 {

if(x > y)
return(x);
return(y);

26 }
27
28 void isLarger(int big)
29 {
30 printf(“Value %d is larger.\n”,big); 31 }
32
33
```

Max is kind of the stalwart of learning C. It is passed two values, and returns the larger of the two. We’ve also added the *isLarger* function, which doesn’t return anything, but we wanted to show how multiple function can be declared within the code. Build and run the code.

Type two different values separated by a space. As you can see, the code displays the larger of the two values. Now, let’s talk