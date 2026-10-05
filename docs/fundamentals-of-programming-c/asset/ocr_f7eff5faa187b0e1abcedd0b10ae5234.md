# 17.5. PROTECTED MEMBERS

![](bbox=[0.318, 0.17, 0.72, 0.387])

Figure 17.6: Inheritance hierarchy of shape classes

```
// File testshapes.cpp

#include <iostream>
#include <vector>

#include "rectangle.h"
#include "triangle.h"
#include "circle.h"
#include "ellipse.h"

using namespace std;

int main() {
    Rectangle rect(3, 4);
    Circle circ(4.5);
    Triangle tri(3, 4, 5);
    Ellipse eli(3, 4);
    vector<Shape ->> shape_list;

    shape_list.push_back(&circ);
    shape_list.push_back(&tri);
    shape_list.push_back(&rect);
    shape_list.push_back(&eli);

    int n = shape_list.size();
    double area_total = 0.0, max_span = 0.0;

    for (int i = 0; i < n; i++) {
```

©2024 Richard L. Halterman Draft date: January 26, 2014