# Chapter 11 A Case Study: Random Numbers 639

Else // the request must be for a floor below the current floor
Display the current floor number
While not at the designated floor
Decrement the floor number
Display the new floor number
While
Display the ending floor number
Endif

This algorithm consists of an if-else statement with three parts:

+   - If an incorrect service is requested, no action is taken.
- If a floor above the current position is selected, the elevator moves up.
- If a floor below the current position is selected, the elevator moves down.

# Step 3 Code the Solution

A suitable function for the preceding algorithm can be coded by a while loop to increment and decrement the elevator's position one floor at a time using a count to report the elevator's position, as follows:

```
void elevator::request(int newfloor)
{
  if (newfloor < 1 || newfloor > maxFloor || newfloor == currentFloor)
    // do nothing
  else if (newfloor > currentFloor) // move elevator up
  {
    cout << "\nStarting at floor " << currentFloor << endl;
    while (newfloor > currentFloor)
    {
      currentFloor++; // add one to current floor
      cout << " Going now at floor " << currentFloor << endl;
    }
    cout << " Stopping at floor " << currentFloor << endl;
  }
  else // move elevator down
  {
    cout << "\nStarting at floor " << currentFloor << endl;
    while (newfloor < currentFloor)
    {
      currentFloor--; // subtract one from current floor
      cout << " Going - now at floor " << currentFloor << endl;
    }
    cout << "Stopping at floor " << currentFloor << endl;
  }
}
```