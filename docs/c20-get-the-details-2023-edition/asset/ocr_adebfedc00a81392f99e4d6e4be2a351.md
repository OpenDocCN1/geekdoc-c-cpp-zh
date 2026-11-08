```
```cpp
64  int main() {
65
66      std::cout << '\n';
67
68      CarElement wheelFrontLeft  = Wheel("front left");
69      CarElement wheelFrontRight = Wheel("front right");
70      CarElement wheelBackLeft   = Wheel("back left");
71      CarElement wheelBackRight  = Wheel("back right");
72      CarElement body            = Body();
73      CarElement engine          = Engine();
74
75      CarElement car = {&wheelFrontLeft, &wheelFrontRight,
76                        &wheelBackLeft, &wheelBackRight,
77                        &body, &engine};
78
79      std::visit(carElementPrintVisitor, engine);
80      std::visit(carElementPrintVisitor, car);
81      std::cout << '\n';
82
83      std::visit(carElementDoVisitor, engine);
84      std::visit(carElementDoVisitor, car);
85      std::cout << '\n';
86
87  }
```
```

The car (line 75) stands for the object hierarchy, and the two operations visit that is carElementPrintVisitor (line 45) and carElementDoVisitor (line 54). Deducing this enables the car-visiting lambda expressions in lines 47 and 58 to reference the implicit lambda object to visit the components of the car: car.visitCarElement(self).

![](bbox=[0.224, 0.651, 0.776, 0.867])

The Overload Pattern