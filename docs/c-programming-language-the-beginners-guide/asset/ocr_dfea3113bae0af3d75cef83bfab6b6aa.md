```
```c
12  printf("%f * %f * %f = %f\n",x,y,z,a); 13
14  return(0);
15  }
17  float product(float a, float b, float c) 18 {
19  return(a * b * c); 20 }
```
```

Save these changes, and then build and run the code. As you can see, the result is the same. A more realistic example is shown in the code below:

```
```c
1  #include 2

•  int max(int x, int y);

•  void isLarger(int big); 5

6  int main()
7  {
8  int a,b,larger;
9
10 printf("Type two integers separated by a space: ");
11 scanf("%d %d",&a,&b);

•  larger = max(a,b);
•  if(a == larger)
```
```