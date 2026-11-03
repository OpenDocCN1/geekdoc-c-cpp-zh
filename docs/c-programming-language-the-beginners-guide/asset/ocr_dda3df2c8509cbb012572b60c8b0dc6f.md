You cannot change the number of elements in an array after the array has been declared. Some tricks exist to work around this limitation. But for now, just accept it as a rule. Also, don't forget that the first element in an array is zero, not 1.

Humans start counting at the C language starts counting at An integer array CALORIES is declared at line 7 in the code below:

+   - int calories[MEALS];
+   - int x,total;
+   - total = 0;
+   - puts("Calorie Counter");
+   - for(x=0;x
+   - printf("Calories at meal %d: ",x+1);
+   - scanf("%d",&calories[x]);
+   - total = total +calories[x]; 17 }

```
1 #include
2
3 #define MEALS 3
4
5 int main()
6 {
9
13 {
18 printf("You had a total of %d calories.\n",total); 19
20 return(0);
21 }
```