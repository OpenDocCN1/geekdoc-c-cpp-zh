![](bbox=[0.115, 0.075, 0.865, 0.575])

# FIGURE 1
An overview of the validation process

When you use a rule set to validate an instance of a specific type or object, the block can apply the rules to:

+   - The type itself
+   - The values of public readable properties
+   - The values of public fields
+   - The return values of public methods that take no parameters

Notice that you can validate the values of method parameters and the return type of methods that take parameters when that method is invoked, only by using the validation call handler (which is part of the Validation block) in conjunction with the Unity dependency injection and interception mechanism. The validation call handler will validate the parameter values based on the rules for each parameter type and any