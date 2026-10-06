# Conditionals

```
scala a & 0xff
scala (a & 0xff).toBinaryString
scala a - 0xff
scala (a - 0xff).toBinaryString
scala (a << 3).toBinaryString
scala ((a >> 8) && 0xff).toBinaryString
```

#  3.8.4 Exercises

+   1. Write Boolean expressions for the following:
(a) Assume you have a variable age changed. Tell if the person is old enough to legally drink.
(b) Given a height in inches, tell if a person can ride an amusement park ride that requires riders to be between 48" and 74".
2. Determine if the following expressions are true or false. Assume the following, a=1, b=2, c=3, d=true, e=false.
(a) a==1
(b) c<b || b>c
(c) a<=c && d==e
(d) 1+2==c
(e) d
(f) !e
(g) d || e
(h) 6-(c-a)==b && (e || d)
(i) c>b && b>a
(j) a!=b==c || (c+a-b==a && c-a>b)
3. Determine if the following expressions are true or false. Assume the following, b=10, x=true, y=false.
(a) x
(b) x && y
(c) a==b-9
(d) a<b || !x
(e) !y && x
(f) (c/b)/b==b
(g) (c+ba==b*b+c) || y
(h) a <= b && b <= c && c >= a
(i) c/(b/b)==b
(j) !(x || y)
4. The reverse method can be called on a String. Use this to write a script where the user inputs a word (use readLine) and you tell them whether or not it is a palindrome.