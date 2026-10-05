Within a box, attributes (normal font) and behaviors/methods (italic font) are listed.

| Car | parked in Aggregation | CarPort |
|---|---|---|
| • Windscreen | | • Door |
| • Tires[4] | | • Roof |
| • drive | | Walls[3] |
| • refuel | | • open |
| Composition | | • close |

**Figure 15.2** An alternative, more informal way to represent the two has-a-relationships.

There are dozens of different ways to represent the relationships between objects. I have only given a very brief overview of two of them here.

# 15.1.3 Is-a Inheritance

With inheritance, you now map an is-a relationship. For example: a VW bus is-a car. That means the following applies:

+   * A VW bus has all the properties that a car has.

+   * Every object that fits the description (or specification) of a VW bus also fits the description of a car.

+   * The description (or specification) of the VW bus is more specific, while that of the car is weaker.

+   * If you expect a car, then it is correct if a VW bus is delivered to you.