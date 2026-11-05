Let’s see how we can change our code to include an abstract class. Note that we will not be running the code, because there is nothing that can be run using an abstract class.

**Step 1)** As a first step, let’s create an abstract class. The class will be called Tutorial and will just have one method. All the code needs to be written in the Program.cs file.

![](bbox=[0.07, 0.3, 0.92, 0.55])

# Code Explanation:-

+   1. We first define the abstract class. Note the use of the abstract keyword. This is used to denote that the class is an abstract class.
+   2. Next, we are defining our method which does nothing. The method must have the keyword called virtual. This means that the method cannot be changed by the child class. This is a basic requirement for any abstract class.

**Step 2)** Now let’s add our child class. This code is added to the Program.cs file.

![](bbox=[0.07, 0.9, 0.92, 0.98])

There is nothing exceptional about this code. We just define a class called ‘Guru99Tutorial’ which inherits the abstract Tutorial class. We then define the