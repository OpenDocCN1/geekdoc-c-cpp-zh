# 11.1 Structures and Structure Variables

```
struct Polygon {
    char name[20]; /* name of a particular type of polygon */
    int n; /* number of vertices */
    float point[10][2]; /* coordinates of the vertices of the
    polygon */
};
```

Instances of type Polygon would be declared as follows.
struct Polygon triangle = {"triangle", 3}, hexagon = {"hexagon", 6};

Because the values are initialized when they are defined, the coordinates of the vertices are initialized to 0.0. The values of the coordinates can be supplied as input data. When they have values, the x and y coordinates of the three vertices of the triangle can be accessed as:

```
x1 = triangle.point[0][0];
y1 = triangle.point[0][1];
x2 = triangle.point[1][0];
y2 = triangle.point[1][1];
x3 = triangle.point[2][0];
y3 = triangle.point[2][1];
```

As arrays may be of any data type, it is possible to declare arrays of structures, which themselves contain arrays, for example,

```
struct Line {
    float p1[2]; /* coordinates of one endpoint of a line */
    float p2[2]; /* coordinates of the other endpoint of a line */
};
```

```
struct Line triangle[3]; /* declare a triangle as having three sides */
```

Then triangle[0] is one side of the triangle; triangle[1] is another side, and triangle[2] is the third side. The sides must, of course, share endpoints or the name triangle is misleading. For example the following defines an actual triangle.

```
triangle[0].p1[0] = 3.5; triangle[0].p1[1] = 5.2; /* point(3.5, 5.2) */
tangle[0].p2[0] = 14.6; triangle[0].p2[1] = 8.9; /* point(14.6, 8.9) */
tangle[1].p1[0] = 3.5; triangle[1].p1[1] = 5.2; /* point(3.5, 5.2) */
```