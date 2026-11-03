```
1 #include 2
3 int main()
4 {
• struct person {
• char name[32];
• int age;
8 };
9 struct person president; 10
10 10 10 10
10 10 10

10 10 10 10 10
10
```

If you can see what's wrong, great. Otherwise, build the code and then check the build log to see the specific error. As you can see, it is incompatible. You cannot use the assignment operator with a string. That is because strings are not variables. They are arrays. Here's how to solve it:

```
• #include
  • #include 3
4 int main()
5 {
• struct person {
• char name[32];
• int age;
```