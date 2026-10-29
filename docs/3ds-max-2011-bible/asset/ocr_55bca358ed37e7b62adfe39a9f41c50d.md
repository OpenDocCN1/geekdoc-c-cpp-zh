# Part IV: Materials, Cameras, and Lighting Basics

You have four options for filtering shadows: Low, Medium, High, and Use Light Smp Range. The Low option renders shadows quickly but isn’t very accurate. The High option takes a while but produces the best quality. The Use Light Smp Range option bases the filtering on the Sample Volume value and can be set to Auto. The Sample Volume can range from 1 to 10,000. The Low option has a Sample Volume value of 8; Medium, 25; and High, 50.

# Note

Only Shadow Map type shadows cast shadows through volume fog.

The Start and End Attenuation values are percentages of the Start and End range values for the light’s attenuation. These values have an impact only if attenuation is turned on for the light.

The Noise settings help to determine the randomness of Volume Light. Noise effects can be turned on and given an Amount. You can also Link the noise to the light instead of using world coordinates. Noise types include Regular, Fractal, and Turbulence. Another option inverts the noise pattern. The Noise Threshold limits the effect of noise. Wind settings affect how the light moves as determined by the wind’s direction, Wind Strength, and Phase.

Figure 20.15 shows several volume light possibilities. The left image includes the Volume Light effect, the middle image enables shadows, and the right image includes some Turbulent Noise.

# FIGURE 20.15

The Volume Light effect makes the light visible.

![](bbox=[0.07, 0.76, 0.78, 0.88])

# Tutorial: Showing car headlights

One popular way to use volume lights is to display the headlights of cars. For this tutorial, you’re going to use the Delfino Feroce 2001 car model created by Viewpoint Datalabs.

To display the headlights of a car, follow these steps:

+   1. Open the Car headlights.max file from the Chap 20 directory on the DVD. This file includes a model of a car.

+   2. Select the Create ⇨ Lights ⇨ Standard Lights ⇨ Target Spotlight menu command, and drag in the Left viewport to create a spotlight object. Select and move the spotlight and the target to be positioned to look as if a light is shining out from the left headlight.

+   3. Open the Modify panel, and in the Spotlight Parameters rollout, set the Hotspot value to 20, the Falloff to 25, and in the Intensity/Color/Attenuation rollout, set the Decay setting to Inverse Square with a Start value of 3.0. In the Atmospheres and Effects rollout, click the Add button, select Volume Light from the Add Atmosphere or Effect dialog box that appears, and click OK.