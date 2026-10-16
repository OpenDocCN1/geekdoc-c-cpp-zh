Two basic operations on a `RandomInt` object are provided that correspond directly to the properties of a (pseudo-)random number generator given above:

+   1. *Construction* (i.e., declaration), which initializes the object to a random number
+   2. *Generation*, which provides the object with a new random number

Additional operations, such as assignment (`=`) and output (`<<`) are also provided. The class is also designed so that any of the operations (numeric, relational, etc.) that can be applied to integers can be applied to class objects, although the result is an `int`, as opposed to a `RandomInt`.

# 7.6.1 Construction

A `RandomInt` object can be constructed by writing a declaration of the form:

```
RandomInt object_name(lower_bound, upper_bound);
```

Such a declaration constructs a RandomInt object named *object_name* whose value is a random number in the range *lower_bound* to *upper_bound*. If *lower_bound* and *upper_bound* are omitted, a random number is generated in the range 0 to some (large) upper limit defined in the RandomInt class.

# 7.6.1.2 Generation

The second operation is to generate a new random number. Given a RandomInt object constructed as just described, this can be done by sending it the `generate()` message:

```
object_name.generate();
```

When this statement is executed, the value of *object_name* is changed to another random integer from the range specified when *object_name* was constructed.⁸ In addition to changing the value of *object_name*, `generate()` returns the randomly generated value.

# 7.6.2 Problem

When the enriched uranium fuel of a nuclear reactor is burned, high-energy neutrons are produced. Some of these are retained in the reactor core, but most of them escape. Because this radiation is dangerous, the reactor must be shielded. We wish to develop a program that simulates neutrons entering the shield and determines what percentage of them get through it.

In our model of the shielding, we will make the simplifying assumption that neutrons entering the shield follow random paths by moving forward, backward, left, or right with equal likelihood, in jumps of one unit. We will also assume that losses of energy occur only when there is a collision that causes a change of direction, and that after a certain number

⁸ Optional arguments *lower_bound* and *upper_bound* can be used with `generate()` to alter the range of the random numbers to be generated.