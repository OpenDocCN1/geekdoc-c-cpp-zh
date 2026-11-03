```
```c
case 'D' : frequency[3][car]++;
    break;
case 'M' : frequency[4][car]++;

    break;

}
/* . . . TABULATION COMPLETED AND PRINTING BEGINS . . . */
printf("\n\n");
printf(" POPULARITY TABLE\n\n");
printf("_________________________\n");
printf("City Ambassador Flat Dolphin Maruti \n");
printf("_________________________\n");
for( i = 1 ; i <= 4 ; i++ )
{
    switch(i)
    {
        case 1 : printf("Bombay ") ;
            break ;
        case 2 : printf("Calcutta ") ;
            break ;
        case 3 : printf("Delhi ") ;
            break ;
        case 4 : printf("Madras ") ;
            break ;
    }
    for( j = 1 ; j <= 4 ; j++ )
        printf("%6d", frequency[i][j] ) ;
    printf("\n") ;
}
printf("_________________________\n");
/* . . . . . PRINTING ENDS. . . . . . . */
```
```

# Output

For each person, enter the city code followed by the car code
Enter the letter X to indicate end.

M 1 C 2 B 1 D 3 M 2 B 4
C 1 D 3 M 4 B 2 D 1 C 3
D 4 D 4 M 1 I 1 B 3 B 3
C 1 C 1 C 2 M 4 M 4 C 2
D 1 C 2 B 3 M 1 B 1 C 2
D 3 M 4 C 1 D 2 M 3 B 4    X

POPULARITY TABLE

| City | Ambassador | Flat | Dolphin | Maruti |
|------|------------|------|---------|--------|
| Bombay | 2 | 1 | 3 | 2 |
| Calcutta | 4 | 5 | 1 | 0 |
| Delhi | 2 | 1 | 3 | 2 |
| Madras | 4 | 1 | 1 | 4 |