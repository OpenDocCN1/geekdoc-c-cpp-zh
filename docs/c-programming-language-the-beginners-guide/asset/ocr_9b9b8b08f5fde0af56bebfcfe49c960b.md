```
```c
1 #include 2
3 void soup(void);
4 {
5 puts("Pea green soup!"); 6 }

7
8 int main()
9 {
• printf("For breakfast I had ");
• soup();
• printf("For lunch I had ");

");
");
```
```

The *sup* function appears above the *main* function. That's okay because the compiler still sees them in a function, and it is always the first function that is executed in the program. What is missing here is the prototype for the *sup* function. Build and run the code.

As you can see, the code outputs text as expected. But try this: move the *sup* function after the *main* function like so:

```
```c
1 #include 2
3
```
```