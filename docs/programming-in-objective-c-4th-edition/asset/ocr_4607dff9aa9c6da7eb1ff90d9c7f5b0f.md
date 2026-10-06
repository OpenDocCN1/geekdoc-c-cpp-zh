```
case '//':
opStr = @" \div ";
break;
}

[self storeFracPart];
firstOperand = NO;
isNumerator = YES;

[displayString appendString: opStr];
display.text = displayString;
}

-(void) storeFracPart
{
  if (firstOperand) {
    if (isNumerator) {
      myCalculator.operand1.numerator = currentNumber;
      myCalculator.operand1.denominator = 1; // e.g. 3 * 4/5 =
    } else
      myCalculator.operand1.denominator = currentNumber;
    }
  } else if (isNumerator) {
    myCalculator.operand2.numerator = currentNumber;
    myCalculator.operand2.denominator = 1; // e.g. 3/2 * 4 =
  } else {
    myCalculator.operand2.denominator = currentNumber;
    firstOperand = YES;
  }
```