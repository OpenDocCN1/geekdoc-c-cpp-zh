```
```c
void main()
{
  int x,y;
  printf("\n Enter 1st number:");
  scanf("%d",&x);
  printf("\n Enter 2nd number:");
  scanf("%d",&y);
  printf("\n GCD is:%d", GCD(x,y));
}
```
```

# **For three numbers**

```
```c
int GCD3 (int x, int y, int z)
{
  return GCD(x, GCD(y, z));
}
```
```

# **Output**

```
```text
Enter 1st number: 10
Enter 2nd number: 5
GCD is: 5

Enter 1st number: 20
Enter 2nd number: 15
GCD is: 5

Enter 1st number: 8
Enter 2nd number: 20
Invalid Input
```
```

# **Related Theory: Logic Used**

# **What is Rotation?**

A rotation is an operation similar to shift except that the bits that fall off at one end are put back to the other end. In C there is no operator for rotation. Instead rotation operation is performed by using bitwise shift operators (<< and >>) and OR operator(|).

# **Left shift**

The expression n << d, the number n is moved d number of bits toward left. While shifting toward left, the left most bits will be lost and 0's will be filled at the right side.