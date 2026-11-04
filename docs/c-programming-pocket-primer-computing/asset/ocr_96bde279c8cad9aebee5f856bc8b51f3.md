```
```c
{
   int a1=40, a2=80, a3=0;
   // ensure the following are true:
   // 1) a1>0 and a1 < 180
   // 2) a2>0 and a2 < 180
   // 3) a1+a1 < 180

   if( ((a1 <= 0) || (a1 >= 180)) ||
       ((a2 <= 0) || (a2 >= 180)) )
   {
      printf("angles out of range: a1 = %d a2 = %d\n", a1, a2);
   }
   else
   {
      if( a1+a2 >= 180)
      {
         printf("a1 + a2 is too large: %d\n", a1+a2);
      }
      else
      {
         a3 = 180 - (a1+a2);
         printf("a1: %d a2: %d a3: %d\n", a1, a2, a3);
      }
   }

   return 0;
}
```
```

> > [Listing 2.7](#) first ensures that a1 and a2 are both between 0 and 180 degrees. If this test succeeds, the next portion of code checks if a1+a2 is at least 180: if so, the values are too large to form a triangle. Otherwise, the value of a3 is set equal to 180-(a1+a2), and the appropriate message is displayed.

This concludes the portion of the chapter involving conditional logic. In [Chapter 1](#) you learned about the scope of variables, and the next several sections