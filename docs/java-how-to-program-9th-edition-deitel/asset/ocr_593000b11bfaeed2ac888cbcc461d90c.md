# 5.4 (Find the Error) Find the error in each of the following code segments, and explain how to correct it:

```
a) i = 1;
while ( i <= 10 );
    ++i;
}
```

```
b) for ( k = 0.1; k != 1.0; k += 0.1 )
    System.out.println( k );
```

```
c) switch ( n )
{
    case 1:
        System.out.println( "The number is 1" );
    case 2:
        System.out.println( "The number is 2" );
        break;
    default:
        System.out.println( "The number is not 1 or 2" );
        break;
}
```

d) The following code should print the values 1 to 10:

```
n = 1;
while ( n < 10 )
    System.out.println( n++ );
```

# Answers to Self-Review Exercises

5.1 a) for, while. b) after. c) switch. d) continue. e) && (conditional AND). f) false. g) static.

5.2 a) False. The default case is optional. If no default action is needed, then there’s no need for a default case. b) False. The break statement is used to exit the switch statement. The break statement is not required for the last case in a switch statement. c) False. Both of the relational expressions must be true for the entire expression to be true when using the && operator. d) True. e) True. f) False. The switch statement does not provide a mechanism for testing ranges of values, so every value that must be tested should be listed in a separate case label. g) True.

```
5.3 a) sum = 0;
    for ( count = 1; count <= 99; count += 2 )
        sum += count;
```

```
b) double result = Math.pow( 2.5, 3 );
```

```
c) i = 1;
while ( i <= 20 )
{
    System.out.print( i );
    if ( i % 5 == 0 )
        System.out.println();
    else
        System.out.print( '\t' );
    ++i;
}
```

```
f) for ( i = 1; i <= 20; i++ )
{
    System.out.print( i );
```