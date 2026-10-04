# 158 Assignment, Formatting, and Interactive Input

```
volts = 12;
cout << " Enter the resistance: " ";
cin >> resistance;
current = volts / resistance;
cout << "The current is " * << current << endl;

return 0;
}


```

+   5. (Heat Transfer) Typically, all objects radiating do so at many different wavelengths. (See the Technical Note in Section 3.5 for a description of wavelength). The wavelength at which an object emits its maximum heat energy can be found using Wein's Law:
\lambda_{max} T = W

\lambda_{max} is the maximum wavelength.
T is the object's temperature in 'K'.
W is Wein's = 2897 microns/K.
a. Using Wein's Law, write a C++ program that accepts an object's temperature in Celsius and outputs the wavelength at which the object radiates its maximum energy. Have your program declare Wein's symbolic constant named WECONSTANT.
b. After verifying that your program is working, use it to determine the maximum heat-wavelength for the sun, Earth, and Mars, with surface temperatures of 5727, 14, and 0.46 degrees Celsius, respectively.

# 3.6 A Case Study: Acid Rain

The use of coal as the major source of steam power began with the Industrial Revolution. Currently, coal is one of the primary sources of electrical generation in many industrialized countries. Since the middle of the 19th century, it has been known that the oxygen used in the burning process combines with the carbon and sulfur in coal to produce carbon dioxide and sulfur dioxide. When these gases are released into the atmosphere, sulfur forms sulfuric acid, which is transformed into hydronium ions and sulfates (see Figure 3.17). The hydronium ions in the atmosphere that fall to Earth are components of rain that change the acidity of lakes and forests.

pH = -log10(concentration of hydronium ions)

The concentration of hydronium ions is measured in units of moles/liter. A pH value of 7 indicates a neutral (neither acid nor alkaline), whereas below 7 indicate the presence of an alkaline substance. For example, sulfuric acid has a pH value of approximately 1, l has a pH value of approximately 13, and distilled water typically has a pH value of 7. Marine life usually can't survive in water with a pH level below 4.