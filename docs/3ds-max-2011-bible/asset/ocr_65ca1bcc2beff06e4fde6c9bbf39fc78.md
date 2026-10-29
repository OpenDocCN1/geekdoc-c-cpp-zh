The Wind object can be used to add a linear force to the scene. The force is directed globally in the direction that is displayed on the Wind object icon, so you need to be careful to place this icon in the correct viewport in order to get the wind blowing in the right direction. The strength of the wind is determined by the Wind Speed value. The wind’s ability to move objects depends on its strength and the object’s Mass value. Heavier objects are harder to blow away.

The Perturb Speed option lets you make the wind gusty. The Variance is how different its strength is from the base value, and the Time Scale determines how often these gusts take place. You can also set a Ripple option to cause a variance in wind strength Left/Right, Up/Down, or Back/Forward with a given Magnitude and Frequency. You can also perturb (or change) time and see the results.

The Use Range lets you specify a range on which the wind has an effect. All objects within the set range are influenced by the wind, but objects beyond the range are not. The Enable Sheltering option lets objects positioned behind other objects be sheltered from the wind. You can choose which objects the wind can affect, including Rigid Bodies, Cloth, Soft Bodies, and Ropes.

# Toy Car

The Toy Car reactor object is a specific object type that simulates a driving car that produces linear motion by rotating wheels. For this object, you can select a Chassis object that represents the car body and pick a list of objects to act as wheels. For this system, you can specify Angular and Linear Strength values and a Suspension value.

You can also specify the car’s orientation using the icon (an arrow points in the direction the car will travel) or using a Common Local Orientation. For the wheels, you can specify to Allow Wheel Penetration, which lets the system have some give as it moves over a rough surface, and whether the wheels spin. To give the car some power, you can set the Angular Speed and Gain of the wheels.

For the reactor version 3 engine, an additional set of parameters is available.

# Tip

If you use the reactor version 3 engine with the Toy Car object, then a new set of parameters for controlling its strength, suspension, and breakable threshold is available.

# Fracture

The Fracture reactor object offers a way to have reactor objects blown apart. The Properties rollout includes a list of Pieces that are to be involved in the fracturing. If you select a Piece from the list, you can designate it as Broken, Normal, Unbreakable, or Keystone, or to Break at Time. The Keystone option is the main piece that causes all pieces to break if this piece breaks. The Now button sets the break time to the current frame.

The Use Connectivity option enables linked objects to stay together, such as two parts connected to a spring. You can also select to Break On and set an Impulse value or a Velocity value. The Energy Loss is the amount of energy lost with every collision.

# Tutorial: Smashing a gingerbread house

It doesn’t matter how many times your mother asks you to not play ball in the house, you always forget. And Murphy’s Law says that you’ll forget at just the wrong time, like when the gingerbread house has just been finished.

To smash a gingerbread house, follow these steps: