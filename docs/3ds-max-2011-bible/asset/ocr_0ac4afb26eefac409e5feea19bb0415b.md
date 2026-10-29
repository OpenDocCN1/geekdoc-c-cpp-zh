# Chapter 46: Using Atmospheric and Render Effects

+   3. With the SphereGizmo still selected, open the Modify panel and click the Add button in the Atmospheres rollout of the Environment and Effects dialog box, which is opened using the Rendering→ Environment menu command or by pressing the 8 key. Select Fire Effect from the Add Atmosphere dialog box, and click OK. Then select the Fire effect, and click the Setup button. The Environment and Effects dialog box opens.

+   4. In the Fire Effects Parameters rollout, leave the default colors as they are—Inner Color yellow, Outer Color red, and Smoke Color black. For the Flame Type, select Tendril with Stretch and Regularity values of 1. Set the Flame Size to 30, the Density to 15, the Flame Detail to 10, and the Samples to 15.

Figure 46.9 shows the resulting sun after it’s been rendered.

# FIGURE 46.9

A sun image created with a simple sphere, a material with a Noise Bump map, and the Fire effect

![](bbox=[0.06, 0.51, 0.74, 0.82])

# Tutorial: Creating clouds

Sky images are fairly easy to find, or you can just take your camera outside and capture your own. The trick comes when you are trying to weave an object in and out of clouds. Although you can do this with a Shadow/Matte mask, it would be easier if the clouds were actual 3D objects. In this tutorial, you’ll create some simple clouds using the Fire effect.

To create some clouds for a sky backdrop, follow these steps: