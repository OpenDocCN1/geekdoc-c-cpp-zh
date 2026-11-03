```
```c
5  printf("Here is a value: 27\\n");
6
7  return(0);
8 }
9
10
```
```

The *printf* function in line 5 of our sample code above generates an output that would have you believe that the number 27 was a value, but it is not. It is part of a string—just the characters 2 and 7. To specify a value, you need to do two things. First, you must place a value into the code—in this case the number

+   - Second, you must direct the *printf* function to display that value.

Edit line five to replace the characters 2 and 7 with ‘%d.’ In some editors, you may see the %d highlighted. That is because it is a special symbol for the *printf* function. It is a placeholder. In this case, it is a placeholder for an integer value—a whole number. Place a comma after the string and add a second argument to the *printf* function: the value 27.

Note how a value is shown in its own color in the Code Blocks editor. The printf function now has two arguments. The first is called the formatting string. It contains one placeholder, which is %d. Matching that placeholder is the second argument: the integer value 27. Your code should now look like this:

```
```c
1 #include 2
3 int main()
4 {
5 printf("Here is a value: %d\\n", 27); 6
```
```