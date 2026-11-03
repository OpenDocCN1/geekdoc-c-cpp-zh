```
    {
        int a=3,b=4,c=3,d=4,x,y;
        x=(a=5)&&(b=7);
        y=(c=5)||(d=8);
        printf("a=%d,b=%d,c=%d,d=%d,x=%d,y=%d\n",a,b,c,d,x,y);
        x=(a==6)&&(b=9);
        y=(c==6)||(d=10);
        printf("a=%d,b=%d,c=%d,d=%d,x=%d,y=%d\n",a,b,c,d,x,y);
    }
```

```
    (18)main()
    {
        int a=10;
        a=a++ + a--;
        printf("%d\n",a);
    }
```

```
    (19)main()
    {
        int a=2,b=2,x,y;
        x=4*(+ +a*2+3);
        y=4*(b+ +2+3);
        printf("a=%d,b=%d,x=%d,y=%d\n",a,b,x,y);
    }
```

# ## Programming Exercise

+   1. Enter the temperature in Celsius and convert that into Fahrenheit.
+   2. Accept the radius of the circle and calculate the area and perimeter of the circle.
+   3. Write a program to accept the number in decimal and print the number in octal and hexadecimal.
+   4. Accept any five digit number and print the value of remainder after dividing by 3.
+   5. Accept any two numbers, if the first number is greater than second then print the sum of these two numbers, otherwise print their difference. Write this program using ternary operator.
+   6. Write a program to accept the principal, rate, and number of years and find out the simple interest.
+   7. Accepts marks in five subject and calculate the total percentage marks.

# ## Answers

+   (1) 6
+   (2) c = 0, d = 1
+   (3) e = 0, f = 6
+   (4) 36
+   (5) 6, 5    6, 4    7, 4    7, 5
+   (6) Error, Expressions like 8++, ++x+, (x+y)- are not valid.
+   (7) a = 5, b = 9, c = 2, d = 8, z = 23
+   (8) a = 4, b = 1, c = 0
+   (9) x = 17, y = 8
+   (10) x = 5, y = 7, z = 12, k = 22