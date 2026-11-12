# EXERCISES

1. Consider the classes Sphere and Ball, as outlined here:

```
class Sphere
{
public:
    ...
    double getArea() const; // Surface area
    void displayStatistics() const;
    ... }; // end Sphere

class Ball : public Sphere
{
public:
    ...
    double getArea() const; // Cross-sectional area
    void displayStatistics() const;
    ... }; // end Ball
```

Suppose that the implementation of each version of displayStatistics invokes the method getArea.

+   a. If mySphere is an instance of Sphere and myBall is an instance of Ball, which version of getArea does each of the following calls to displayStatistics invoke? Explain your answer.
+   
+   mySphere.displayStatistics();
+   myBall.displayStatistics();

+   b. If the statements
+   
+   Sphere* spherePtr;
+   Ball* ballPtr;
+   
+   declare spherePtr and ballPtr, which version of getArea does each of the following calls to displayStatistics invoke? Explain your answer.
+   
+   spherePtr->displayStatistics();
+   spherePtr = ballPtr;
+   spherePtr->displayStatistics();
+   ballPtr->displayStatistics();

2. Define and implement a class Pen that has an instance of Ball as one of its members. Provide several members for the class Pen, such as the data member color and methods isEmpty and write.

3. Consider the following classes:

+   • LandVehicle represents a vehicle that travels on land. Its public methods include wheelCount and speed.
+   • MotorizedLandVehicle represents a land vehicle that has a motor. Its public methods include engineCapacity and fuelType.

+   a. Which of the methods mentioned previously can the implementation of speed invoke?
+   b. Which of the methods mentioned previously can the implementation of engineCapacity invoke?