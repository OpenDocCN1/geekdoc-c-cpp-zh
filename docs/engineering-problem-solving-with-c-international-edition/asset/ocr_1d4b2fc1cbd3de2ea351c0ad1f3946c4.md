# switch statement:

```
switch (op_code)
{
case 'n': case 'r':
    printf("Normal operating range \\n");
    break;
case 'm':
    printf("Maintenance needed \\n");
    break;
default:
    printf("Error in code value \\n");
    break;
}
```

# while loop:

```
while (degrees <= 360)
{
    radians = degrees*PI/180;
    printf("%6.0f %9.6f \\n",degrees,radians);
    degrees += 10;
}
```

# do/while loop:

```
do
{
    radians = degrees*PI/180;
    printf("%6.0f %9.6f \\n",degrees,radians);
    degrees += 10;
} while (degrees <= 360);
```

# for loop:

```
for (degrees=0; degrees<=360; degrees+=10)
{
    radians = degrees*PI/180;
    printf("%6.0f %9.6f \\n",degrees,radians);
}
```

# break statement:

```
break;
```

# continue statement:

```
continue;
```

# File open function:

```
sensor = fopen("sensor1.txt", "r");
waves = fopen(FILENAME,"w");
```