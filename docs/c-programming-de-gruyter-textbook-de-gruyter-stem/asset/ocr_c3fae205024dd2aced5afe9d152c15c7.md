ConcreteCost = (PoolRim.Area() - Pool.Area())*ConcretePrice;
cout << "Concrete Cost is $\$" << ConcreteCost << endl;

Running result:

```
Enter the radius of the pool: 10
Fencing Cost is $2858.85
Concrete Cost is $4335.39
```

When running the main function, we first define three variables of type float. After reading the radius of the pool, we create an object Pool using the constructor to initialize its data member with the input value. Then we create the second object PoolRim to represent the fence. The two objects call their function members respectively, and then the problem is solved.

# 4.4 Combination of Classes

Lots of problems in the real world are too complicated to imagine, but complex problems can be divided into simpler subproblems. By gradual division, we can finally describe and solve the problem. This method of division and combination has been widely used in industry for a long time. For example, an important part of television is the kinoscope, and many TV factories choose to buy kinoscopes from special kinoscope producers instead of producing kinoscopes themselves. At the same time, a kinoscope producer may sell kinoscopes to many TV factories. Through specialization and coordination, productivity is largely improved. Now an important way to improve the productivity of software is to achieve the industrial production of software. In object-oriented programming design, we can divide and abstract complex object into a combination of simpler objects, and it using component objects that are easy to understand and implement.

# 4.4.1 Combination

We have always used the method of combination to build a class, so let's see the class Circle below:

```
class Circle //define class Circle, its data and functions
public:
//external interface
Circle(float r); //constructors
float Circumference(); //compute circumference
float Area(); //computer area
```