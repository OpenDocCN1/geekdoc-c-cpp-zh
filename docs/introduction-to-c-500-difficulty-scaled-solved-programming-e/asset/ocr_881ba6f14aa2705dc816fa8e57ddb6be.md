```
if(i > j)
  max = i;
else
  max = j;
if(k > max)
  max = k;
if(m > max)
  max = m;
```

```
std::cout << "Max: " << max;
return 0;
```

**Comments:** To display the lowest price we change the > to <.

# C.5.6 A water supply company charges the water consumption, as follows:

+   - Fixed amount of $10.
- For the first 30 cubic metres, $0.6/m³.
- For the next 20 cubic metres, $0.8/m³.
- For the next 10 cubic metres, $1.1/m³.
- For every additional metre, $1.2/m³$.

Write a program that reads the water consumption in cubic metres and displays the total cost. For example, if the consumption is 55 cm, the final cost is calculated as follows: cost = 10 + 30*0.6 + 20.8*5.1.

```
#include <iostream>
using std::cout;
using std::cin;

int main() {
  float meters, cost;

  cout << "Enter meters: ";
  cin >> meters;

  /* I don't do the fixed multiplications, to show in detail the method of the cost calculation. */
  if(meters <= 30)
    cost = 0.6*meters;
  else if (meters <= 50)
    cost = 0.6*30 + 0.8*(meters-30);
  else if (meters <= 60)
    cost = 0.6*30 + 0.8*20 + 1.1*(meters-50);
  else
    cost = 0.6*30 + 0.8*20 + 1.1*10 + (meters-60)*1.2;

  cost += 10;
  cout << "Cost: " << cost << '\\n';
  return 0;
}
```