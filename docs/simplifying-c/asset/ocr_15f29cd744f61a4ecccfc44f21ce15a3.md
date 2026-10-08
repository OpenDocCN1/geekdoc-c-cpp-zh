```
printf("\nthe address stored in *(i_arr + 1) + 2 is %u", *(i_arr+1)+2);
printf("\nthe address stored in *(i_arr + 2) + 0 is %u
",*(i_arr+2)+0);
printf("\nThe address stored in *(i_arr + 2) + 1 is %u
",*(i_arr+2)+1);
printf("\nthe address stored in *(i_arr + 2) + 2 is %u
",*(i_arr+2)+2);

/* Print values of array element */
printf("\n\nVALUE OF ARRAY ELEMENTS\n");
printf("\nThe value stored in *(*(i_arr + 0) + 0) is %u",*(*(i_arr + 0)+0));
printf("\n\nThe value stored in *(*(i_arr + 0) + 1) is %u",*(*(i_arr + 0)+1));
printf("\n\nThe value stored in *(*(i_arr + 0) + 2) is %u",*(*(i_arr + 0)+2));

printf("\n\nThe value stored in *(*(i_arr + 1) + 0) is %u",*(*(i_arr+1)+0));
printf("\n\nThe value stored in *(*(i_arr + 1) + 1) is %u",
*(*(i_arr+1)+1));
printf("\nThe value stored in *(*(i_arr + 1) + 2) is %u",
*(*(i_arr+1)+2));
printf("\n\nThe value stored in *(*(i_arr + 2) + 0) is %u
",*(i_arr+2)+0));
printf("\nThe value stored in *(*(i_arr + 2) + 1) is %u
",*(i_arr+2)+1));
printf("\n\nThe value stored in *(*(i_arr + 2) + 2) is %u
\n",*(i_arr+2)+2));
return;
}
/* End of function main */
```

**Output:**

```
ADDRESS OF ARRAY ELEMENTS
The address stored in *(i_arr + 0) + 0 is 65508
The address stored in *(i_arr + 0) + 1 is 65512
The address stored in *(i_arr + 0) + 2 is 65516

The address stored in *(i_arr + 1) + 0 is 65520
The address stored in *(i_arr + 1) + 1 is 65524
The address stored in *(i_arr + 1) + 2 is 65528

The address stored in *(i_arr + 2) + 0 is 65532
The address stored in *(i_arr + 2) + 1 is 65536
The address stored in *(i_arr + 2) + 2 is 65540

ADDRESS OF ARRAY ELEMENTS
The value stored in *(*(i_arr + 0) + 0) is 45
The value stored in *(*(i_arr + 0) + 1) is 60
The value stored in *(*(i_arr + 0) + 2) is 12

The value stored in *(*(i_arr + 1) + 0) is 43
The value stored in *(*(i_arr + 1) + 1) is 44
The value stored in *(*(i_arr + 1) + 2) is 65

The value stored in *(*(i_arr + 2) + 0) is 57
The value stored in *(*(i_arr + 2) + 1) is 18
The value stored in *(*(i_arr + 2) + 2) is 32
```