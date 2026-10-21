as floating-point numbers and provides access to the data via accessor methods (getTemperature() and getDistance()). You can create new SensorData objects using the constructor, passing it the current temperature and distance.

Processing is an object-oriented programming language and allows us to define new classes using the **class** keyword. Classes have a name and they contain data (often called *attributes* or *properties*) and functions (often called *methods*). Our SensorData class contains two attributes named temperature and distance. They are both of type **float**, and we have declared them both **private**. Now only members of the SensorData class are allowed to access them. This is considered good style, because it prevents unwanted side effects and makes future changes much easier. A class should never expose its innards.

To set and get the values of our attributes, we have to use public methods, and our class has three of them: SensorData(), getTemperature(), and getDistance(). (Java and C++ programmers should note that in Processing everything is public if not specified otherwise!) A method that has the same name as the class is called a *constructor*, and you can use it for creating and initializing new objects of that particular class. Constructors do not have return values, but they may specify parameters. Ours, for example, takes two arguments and uses them to initialize our two attributes.

There’s a small problem, though: our method’s parameters have the same names as our classes’ attributes. What would happen if we simply assigned the method parameters to the attributes like this:

```
temperature = temperature;
distance = distance;
```

Right: we simply assigned every method parameter to itself, which is effectively a no-operation. That’s why we use the **this** keyword. It refers to the class itself, so we can distinguish between the method parameters and the classes’ attributes. Alternatively, we could have used different names for the method parameters or the attributes, but I prefer to use **this**.

After the constructor, we define the methods getTemperature and getDistance. Their definitions are very similar; we declare the method’s return type (**float**), the method’s name, and a list of parameters in parentheses. In our case, the parameter list is empty. In the methods, we return the