# Listing 11-3 (continued)

```
System.out.print("Which month? ");
month = keyboard.nextInt();

switch (month) {
case 1:
case 3:
case 5:
case 7:
case 8:
case 10:
case 12:
    numberOfDays = 31;
    break;

case 4:
case 6:
case 9:
case 11:
    numberOfDays = 30;
    break;

case 2:
    System.out.print("Leap year (true/false)? ");
    isLeapYear = keyboard.nextBoolean();
    if (isLeapYear) {
        numberOfDays = 29;
    } else {
        numberOfDays = 28;
    }
}

System.out.print(numberOfDays);
System.out.println(" days");

keyboard.close();
}
```

Figure 11-4 shows several runs of the program in Listing 11-3. For month number 6, the computer jumps to case 6. There are no statements inside the case 6 clause, so that part of the program's run is pretty boring.