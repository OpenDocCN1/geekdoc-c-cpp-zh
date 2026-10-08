for all units of each part and store it in an array. Compute the total units and the
total cost of all parts.

# Pseudocode

```
main:
  call funcinput1()
  call funcinput2()
  call funccompute()
  call functotunits()
  call functotcost()
  call funcoutput()
  stop
```

```
funcinput1:
  for each part
    Input the 5 digit part id, number of units, unit cost
  end for
  return
```

```
funccompute:
  for each part id
    tot-unit-cost ← units * unit cost
  end for
  return
```

```
functotunits:
  total_units ← 0
  for each part id
    tot_units ← tot_units + units
  end for
  return
```