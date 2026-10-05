# 9.4. FUNCTION EXAMPLES

```
cout << "|" << "" << endl;
cout << "|" * "|" << endl;
break;
case 3:
cout << "|" * * << "|" << endl;
cout << "|" * "|" << endl;
cout << "|" * " << "" << endl;
break;
case 4:
cout << "|" * * << "|" << endl;
cout << "|" * "|" << endl;
cout << "|" * * << "|" << endl;
break;
case 5:
cout << "|" * * << "|" << endl;
cout << "|" * "|" << endl;
cout << "|" * * << "|" << endl;
break;
case 6:
cout << "|" * * * << "|" << endl;
cout << "|" * * << "" << endl;
cout << "|" * * << "" << endl;
break;
default:
cout << " *** Error: illegal die value ***" << endl;
}
cout << "+----------+" << endl;

```

+   * roll Returns a pseudorandom number in the range 1..6

```
int roll1() {
    return rand() % 6 + 1;
}
```

+   * Simulates the roll of a die three times

```
int main() {
    // Initialize the die
    initialize_die();

    // Roll the die three times
    for (int i = 0; i < 3; i++)
        show_die(roll());
}
```

In Listing 9.12 (betterdie.cpp), main is no longer concerned with the details of pseudorandom number generation, nor is it responsible for drawing the die. These important components of the program are now