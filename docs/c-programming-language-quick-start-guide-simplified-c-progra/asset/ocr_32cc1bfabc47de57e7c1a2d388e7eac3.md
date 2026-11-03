# 5.7.1 Equalizers

```
```c
void printTable( int );
void printHeading();
void main(void)
{
printHeading();
int x = 1;
for(x=1;x<=10;x++)
{
printTable(x);
}
system("pause");
}
void printTable(int a)
{
for(int x=1; x<=10; x++)
{
printf("%d\t",x*a);
}
printf("\n");
```
```