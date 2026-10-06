```
Fraction *result;

switch (op) {
    case '+':
        result = [operand1 add: operand2];
        break;
    case '-':
        result = [operand1 subtract: operand2];
        break;
    case '*':
        result = [operand1 multiply: operand2];
        break;
    case '/':
        result = [operand1 divide: operand2];
        break;
}

accumulator.numerator = result.numerator;
accumulator.denominator = result.denominator;

return accumulator;
}

@\;end
```

# Designing the UI

For this project, your nib file is called Fraction_CalculatorViewController.xib. You'll design your interface by selecting this file and laying out the buttons and label as