```
int denominator;
}
-(void) print
{
  NSLog("%i/%i", numerator, denominator);
}
-(void) setNumerator: (int) n
{
  numerator = n;
}
-(void) setDenominator: (int) d
{
  denominator = d;
}
```

@end
print method uses NSLog to display the values of the instance variables numerator and denominator. But to which numerator and denominator does this method refer? It refers to the instance variables contained in the object that is the receiver of the message. That's an important concept, and we return to it shortly.

setNumerator: method stores the integer argument called n in the instance variable numerator. Similarly, setDenominator: stores the value of its argument d in the instance variable denominator.

# The program Section

The program section contains the code to solve your particular problem, which can be spread out across many files, if necessary.