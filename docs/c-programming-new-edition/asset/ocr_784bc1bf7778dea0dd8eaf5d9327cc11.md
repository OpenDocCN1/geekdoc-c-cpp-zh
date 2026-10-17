```
```c
{
    case 'I':
        return 1;
    case 'V':
        return 5;
    case 'X':
        return 10;
    case 'L':
        return 50;
    case 'C':
        return 100;
    case 'D':
        return 500;
    case 'M':
        return 1000;
    default:
        return 0;
}
}

// Function to convert a Roman numeral string to its decimal equivalent
int romanToDecimal(char *roman)
{
    int decimal = 0;
    int prevValue = 0;

    // Iterate through the Roman numeral string from right to left
    for (int i = strlen(roman) - 1; i >= 0; i--)
    {
        int currentValue = romanCharToDecimal(roman[i]);
        // If the current value is smaller than the previous value, subtract it
        if (currentValue < prevValue)
        {
```
```