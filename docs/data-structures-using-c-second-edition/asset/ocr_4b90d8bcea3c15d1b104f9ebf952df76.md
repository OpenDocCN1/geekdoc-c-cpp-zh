```
getch();
return 0;
}
void insert_val()
{
int val, f = 0;
printf( "\nEnter the element to be inserted : " );
scanf( "%d", &val );
key = ( val % 10 ) - 1;
if ( ht[key] == -1 )
{
ht[key] = val;
}
else
{
if ( key < 9 )
{
for ( i = key + 1;i < 10;i++ )
{
if ( ht[i] == -1 )
{
ht[i] = val;
break;
}
}
}
for ( i = 0;i < key;i++ )
{
if ( ht[i] == -1 )
{
ht[i] = val;
break;
}
}
}
}
```

```
void display()
{
for ( i = 0;i < 10;i++)
printf( "\t%d", ht[ i ] );
}
```

```
void search_val()
{
int val, flag = 0;
printf( "\nEnter the element to be searched : " );
scanf( "%d", &val );
key = ( val % 10 ) - 1;
if ( ht[ key ] == val )
flag = 1;
else
{
for ( i = key + 1;i < 10;i++ )
{
if(ht[i] == val)
{
flag = 1;
key = i;
break;
}
}
```