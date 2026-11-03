Output:- No, continue can work only with loops and not switch.

# 9.

```
char card = 3;
switch(card)
{
    case 1: printf("\n King");
    case 2: printf("Queen");
    default: printf("Jokar");
}
printf("\nYou have losing the game:");
```

Output:- Joker
You have lost the game:

In the above program the case variable is card that value is 3. and there is no case constant that is 3 so no perfect match here and compiler execute the printf( ) statement after the default that print out “Jokar” and then control comes out to the switch block when comes out met with a printf( ) statement that print “You have lost the game”.

# 10.

```
int prize = 3;
switch(prize)
{
    case ‘3’: printf("\nSilver:"); break;
    case 3: printf("\nGold") break;
```

vice versa.

# 19.

```
int k=35;
printf("%d %d %d",k==35,k=50,k>40);
```

Output:-0 50 0

When printf( ) statement is executed the first the expression and comparison take place and the expression is solved from right to left order so first condition (k>40) is checked because k = 35 so it becomes false and gives 0. now continuing in order right to left next k = 50 is executed and it assigns 50 in k and now k is compared with 35 that gives false because k is 50 not equal 35 and gives 0. and printing will take place from left to right.

# 20.

```
int a=97;
char b='a';
if(a==b) printf("hello matrix");
else printf("bye matrix");
```

Output:-hello matrix

here a and b are compared against equality but b contains ‘a’ that ASCII value is 97. so both a and b are equal and condition becomes true and gets execute the statement next to the if statement.

# 21.

```
int x = 15;
printf("%d %d %d ",x!=15,x=20,x<30);
```

Output:-1 20 1