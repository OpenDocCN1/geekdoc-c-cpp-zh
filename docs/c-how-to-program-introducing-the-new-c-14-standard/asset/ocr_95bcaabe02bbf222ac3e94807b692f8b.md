copy, we do not have to increment or decrement separate copies of `martianCount` for each `Martian` object.

![](bbox=[0.123, 0.183, 0.196, 0.235])

# Performance Tip 9.5

Use `static` data members to save storage when a single copy of the data for all objects of a class will suffice—such as a constant that can be shared by all objects of the class.