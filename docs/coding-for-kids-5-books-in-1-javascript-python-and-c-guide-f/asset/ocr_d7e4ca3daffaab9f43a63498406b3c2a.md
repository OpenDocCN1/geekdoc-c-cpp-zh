```
```python
carNames = [ 'Toyota', 'Ford', 'BMW', 'Ferrari', 'Porsche']

for car in carNames:
    print("Car is ", car)
```
```

We use the ‘in’ keyword. The variable car iterates over the list and takes each element’s value.

+   - During the first execution of the loop, car has the value ‘Toyota’
+   - During the second execution of the loop, car has the value ‘Ford’
+   - During the third execution of the loop, car has the value ‘BMW’
+   - and so on.

The loop keeps on executing as long as there are elements present in the list.

A list can have duplicate values and it can have string values, integer values, boolean values, float values or a mix.

```
```python
list1 = [ 1, 'test', True, False, 9.1, 1, 'test']
for element in list1:
    print("The element is ",element)
```
```

In the above piece of code, list1 has a mix of different types of variables and duplicate values. Below is the output for the print statement