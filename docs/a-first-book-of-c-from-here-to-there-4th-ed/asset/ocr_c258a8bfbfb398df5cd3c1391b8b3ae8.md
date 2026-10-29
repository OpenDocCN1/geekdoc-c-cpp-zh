```
{ elNum = idnum; currentFloor = cfloor; highestFloor = maxFloor; } void Elevator::request(int newfloor) { if (newfloor < 1 || newfloor > highestFloor || newfloor == currentFloor) ; // do nothing else if (newfloor > currentFloor) // move elevator up { cout << "\nElevator " << elNum << " starting at floor " << currentFloor << endl; while (newfloor > currentFloor) { currentFloor++; // add one to current floor cout << " Going Up - now at floor " << currentFloor << endl; } cout << "Elevator " << elNum << " stopping at floor " << currentFloor << endl; } else // move elevator down { cout << "\nElevator " << elNum << " starting at floor " << currentFloor << endl; while (newfloor < currentFloor) { currentFloor--; // subtract one from current floor cout << " Going Down - now at floor " << currentFloor << endl; } cout << "Elevator "<< elNum << " Stopping at floor " << currentFloor << endl; } return; }
```

```
int main() { Elevator a; // declare 1 object of type Elevator a.request(6); a.request(3); return 0; }
```