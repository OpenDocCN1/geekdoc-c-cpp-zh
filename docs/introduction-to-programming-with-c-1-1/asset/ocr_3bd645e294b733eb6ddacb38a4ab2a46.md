```
int i;

double number, sum =0.0;

for(i=1; i <=10;++i)
{
printf("Enter a n%d: ",i);
scanf("%lf",&number);

// If user enters negative number, loop is terminated
if(number <0.0)
{
continue;
}

sum+= number;// sum = sum + number;
}

printf("Sum = %.2lf",sum);

return0;
}
```

# Output

```
Enter a n1: 1.1

Enter a n2: 2.2

Enter a n3: 5.5

Enter a n4: 4.4

Enter a n5: -3.4
```