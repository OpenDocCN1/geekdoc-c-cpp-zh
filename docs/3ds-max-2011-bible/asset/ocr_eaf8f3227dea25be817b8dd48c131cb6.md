# Part XI: Advanced Lighting and Rendering

The Regularity value determines how much of the Atmospheric Apparatus is filled. The spherical gizmos in the previous figures were all set to 0.2, so the entire sphere shape wasn't filled. A setting of 1.0 adds a spherical look to the Fire effect because the entire gizmo is filled. For a more random shape, use a small Regularity value.

The Flame Size value affects the overall size of each individual flame (though this is dependent on the gizmo size as well). The Flame Detail value controls the edge sharpness of each flame and can range from 1 to 10. Lower values produce fuzzy, smooth flames, but higher values result in sharper, more distinct flames.

The Density value determines the thickness of each flame in its center; higher Density values result in flames that are brighter at the center, while lower values produce thinner, wispy flames. Figure 46.8 shows the difference caused by Density values of, from left to right, 10, 20, 50, and 100.

# FIGURE 46.8

The Fire effect brightness is tied closely to the flame's Density value.

![](bbox=[0.08, 0.6, 0.78, 0.78])

The Samples value sets the rate at which the effect is sampled. Higher sample values are required for more detail, but they increase the render time.

The Motion section includes options for setting the Phase and Drift of a fire effect. The Phase value determines how wildly the fire burns. For a wild, out-of-control fire, animate the Phase value to change rapidly. For a constant, steady fire, keep the value constant throughout the frames. The Drift value sets the height of the flames. High Drift values produce high, hot-burning flames.

When the Explosion check box is selected, the fire is set to explode. The Start and End Times for the explosion are set in the Setup Explosion Phase Curve dialog box that opens when the Setup Explosion button is clicked. If the Smoke option is checked, then the fire colors change to the smoke color for Phase values between 100 and 200. The Fury value varies the churning of the flames. Values greater than 1.0 cause faster churning, and values lower than 1.0 cause slower churning.

# Tutorial: Creating the sun

You can use the Fire effect to create a realistic sun. The modeling part is easy—all it requires is a simple sphere—but the real effects come from the materials and the Fire effect.

To create a sun, follow these steps:

+   1. Open the Sun.max file from the Chap 46 directory on the DVD.
+      This file contains a simple sphere with a bright yellow material applied to it.
+   2. Select Create > Helpers > Atmospherics > Sphere Gizmo, and drag a sphere in the Front viewport that encompasses the "sun" sphere.