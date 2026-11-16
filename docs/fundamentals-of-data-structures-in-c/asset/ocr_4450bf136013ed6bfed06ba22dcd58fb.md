```
printf("Enter the order of matrix : ");
scanf("%d %d", &m, &n);
printf("Enter the elements of matrix : ");
for(i = 0 ; i < m ; i++)
for(j = 0 ; j < n ; j++)
scanf("%d", &a[i][j]);
for(i = 0 ; i < m ; i++)
for(j = 0 ; j < n ; j++)
sum = sum + a[i][j];
printf("Sum of elements of the matrix is %d", sum);
}
```

The program displays the following output
Enter the order of matrix : 2 2
Enter the elements of matrix : 1 1 1 1
Sum of elements of the matrix is 4

In Program 1.16 we have used an array “a” and assigned 4 (4x2) elements of type int. The program displays the values and addresses of the memory occupied by the elements of the array matrix. Since the array is of type int each element in the array occupies 2 bytes of memory.

# Initializing an array using loops

An array can be initialized by using a for loop, a while loop or a do-while loop. The following examples illustrate the use of initializing an array using for loops.

# Examples for initializing an array using a for loop

+   1. int i, j, x = 5, mark[10][5];
+   for(i = 0 ; i < 10 ; i++)
+   for(j = 0 ; j < 5 ; j++)
+   {
+   mark(i][j] = x;
+   x += 5;
+   }

+   2. int i, j, mark[10][5];
+   for(i = 0 ; i < 10 ; i++)
+   for(j = 0 ; j < 5 ; j++)
+   scanf("%d", &mark[i][j]);

In the first example, the for loop initializes the value 5 to the variable mark[0][0], 10 to the variable mark[0][1] and so on. In the second example, the scanf() function reads values from the user for the array. Similarly, arrays can also be initialized using while loop and do-while loops.