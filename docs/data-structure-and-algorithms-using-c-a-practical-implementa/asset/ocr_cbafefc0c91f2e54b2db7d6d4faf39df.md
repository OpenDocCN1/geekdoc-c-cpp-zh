```
arr[i] = value;
}
cout<<"\n Step = "<<step;
step++;
for(p = 1; p < n; p++)
cout<setw(5)<<arr[p];
}
}
void display(int arr[], int n)
{
int i;
for(i = 1 ; i <= n; ++ i)
{
cout<<setw(5)<<arr[i];
}
}
```

# OUTPUT

```
Enter number of elements?
Size of the list:
Enter a number:25
Enter a number62
Enter a number8
Enter a number93
Enter a number5
Enter a number:
Enter a number45
Entered list is as follows:
25 62 8 93 5 7 45
Heap tree is
93 62 45 25 5 7 8
Step = 1 62 25 45 5 8 5 7 93
Step = 2 45 25 7 7 8 5 62 93
Step = 3 25 5 8 7 5 45 62 93
Step = 4 8 5 5 7 25 45 62 93
Step = 5 7 5 8 25 45 62 93
Step = 6 5 7 8 25 45 62 93
Sorted list is as follows :
5 7 8 25 45 62 93
Process exited after 9.935 seconds with return value 0
Press any key to continue . . .
```