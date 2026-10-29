# 4. (Program) Heat is radiated from the sun and all planets orbiting the sun. The heat that's radiated can be calculated by using the following formula:

E = ε σ T⁴

+   - E is the energy radiated per second in units of watts per meter squared (watts/m²).
+   - ε is the emissivity of the substance, which is 1 for the sun and all the planets.
+   - σ is the constant (.000000056697 = 5.6697e-8).
+   - T is the surface temperature in degrees Celsius.

For example, the heat radiated from the sun, which has an emissivity of 1 and a surface temperature of approximately 6000° C, is as follows:

E = (1) × (.000000056697) × (6000)⁴ watts/m²
= 73,479,300 watts/m²

Using the formula, write a C++ program that accepts a planet's temperature and provides the heat generated from the planet as its output. Your program should assign the value 5.6697e-8 to a symbolic constant named HEATFACTOR. After determining that your program is working correctly (make sure it produces the correct radiation for the sun), use it to complete the following chart:

| Planet (emissivity = 1) | Average Surface Temperature (° Celsius) | Heat Radiated (watts/m²) |
|---|---|---|
| Mercury | 270 | |
| Venus | 462 | |
| Earth | 14 | |

# 5. (Program) During the day, heat is absorbed by many objects, such as cars, roofs, and brick walls. This heat is then radiated back into the environment during the cooler evening hours. Using the formula E = ε σ T⁴ (see Exercise 4), write a C++ program that determines the amount of heat radiated for the objects listed in the following table. Your program should request the object's average surface temperature and emissivity, and then calculate and display the heat radiated. Make sure to use a symbolic constant named HEATFACTOR for the value of σ. Complete the following chart, making three runs of the program:

| Substance | Average Surface Temperature (° Celsius) | Emissivity | Heat Radiated (watts/m²) |
|---|---|---|---|
| Automobile | 47 | .3 | |
| Brick | 45 | .9 | |
| Commercial roof | 48 | .05 | |