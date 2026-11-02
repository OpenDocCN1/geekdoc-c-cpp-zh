Here is a sample map:

* * * *   * * *
  * * * * * * *
* * * *   * * *
* * * * * * * *
* * * * * * * *
* *   * * * * *
* * * * * * *
  * * * * *
* * *

![](bbox=[0.65, 0.1, 0.9, 0.3])

© nicolamargaret/Stockphoto.

Then write a program that reads one hundred terrain height values and shows how the terrain gets flooded when the water level increases in ten steps from the lowest point in the terrain to the highest.

# Engineering P6.16

Write a program that models the movement of an object with mass m that is attached to an oscillating spring. When a spring is displaced from its equilibrium position by an amount x, Hooke's law states that the restoring force is

F = -kx

where k is a constant that depends on the spring, (Use 10 N/m for this simulation.) Start with a given displacement x (say, 0.5 meter). Set the initial velocity v to 0. Compute the acceleration a from Newton's law (F = ma) and Hooke's law, using a mass of 1 kg. Use a small time interval Δt = 0.01 second. Update the velocity—it changes by aΔt. Update the displacement—it changes by vΔt.

Every ten iterations, plot the spring displacement as a bar, where 1 pixel represents 1 cm. Use the Picture class from the media/picture directory of the companion code for creating an image.

![](bbox=[0.78, 0.5, 0.95, 0.7])

![](bbox=[0.45, 0.78, 0.65, 0.88])

# Media P6.17

Sounds can be represented by an array of "sample values" that describe the intensity of the sound at a point in time. The code in the media/sound directory of the companion code allows you to modify a sound file. Your task is to introduce an echo. For each sound value, add the value from 0.2 seconds ago. Scale the result so that no value is larger than 32767.

![](bbox=[0.75, 0.8, 0.95, 0.95])

© GordonHeeley/Stockphoto.

Media P6.18 Using the sound processing code from the media/sound directory of the companion code, write a program that reverses the sample values in a sound file.

Media P6.19 Using the sound processing code from the media/sound directory of the companion code, write a program that computes the average and maximum sample value of a