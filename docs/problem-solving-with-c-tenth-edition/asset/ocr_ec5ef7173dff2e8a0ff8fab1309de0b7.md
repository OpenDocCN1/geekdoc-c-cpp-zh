# EXAMPLE

```
case Constant_2:
    Statement_Sequence_2
    break;
.
.
.
case Constant_n:
    Statement_Sequence_n
    break;
default:
    Default_Statement_Sequence }

int vehicleClass;
cout << "Enter vehicle class: ";
cin >> vehicleClass;

switch (vehicleClass)
{
    case 1:
        cout << "Passenger car.";
        toll = 0.50;
        break;
    case 2:
        cout << "Bus.";
        toll = 1.50;
        break;
    case 3:
        cout << "Truck.";
        toll = 2.00;
        break;
    default:
        cout << "Unknown vehicle class!";
}
```

# PITFALL Forgetting a break in a switch Statement

If you forget a break in a switch statement, the compiler will not issue an error message. You will have written a syntactically correct switch statement, but it will not do what you intended it to do. Consider the switch statement in the box entitled "switch Statement." If a break statement were omitted, as indicated by the arrow, then when the variable vehicleClass has the value 1, the case labeled

```
case 1:
```