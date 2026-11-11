chance to reuse them at a later stage. Whereas, the other two members (`roll_no` and `marks`) are specific to class `Student`, and there is no chance to reuse them. Such members are called **specialized members**. If we think from the perspective to facilitate reusability in future, it would be a good idea to define the generic members in a **parent class** (named as `Person`) and keep only the specialized members in the child class `Student`, as shown in the Figure 14.25. Such an inheritance with a single parent class and a single child class is called **single level inheritance**. Therefore, class `Student` will have name, dob, gender, `roll_no`, and `marks` out of which the members name, dob, and gender are inherited from the parent class `Person`. We can always create the members name, dob, and gender as **protected** in `Person`, so that they can be directly accessed in the child class `Student`. The advantage of this design is that, if we wish to plug one more class in future (say `Professor`) we can do this by simply creating it as another child class of `Person`, and it will inherit the generic members without putting any special effort.

![](bbox=[0.293, 0.397, 0.7, 0.646])

The implementation of this hierarchy requires class `Date` to be created as an user-defined data type whose object can store the date of birth. We have implemented class `Date` in section 14.5

**Figure 14.25:** An example of single level inheritance

# ## 14.4.2 Hierarchical inheritance

This is a relationship of inheritance created with **single parent class having more than one child classes** as shown in Figure 14.26.

![](bbox=[0.315, 0.833, 0.867, 0.951])

**Figure 14.26:** Hierarchical inheritance