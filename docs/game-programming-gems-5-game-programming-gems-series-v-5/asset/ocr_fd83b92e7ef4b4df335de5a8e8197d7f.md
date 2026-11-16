We compute the stretch factor, described in Equation 5.2.2, based on \( Vec_{precip} S_f \) (a precomputed scale factor to scale down successive textures so they appear further away), \( C_{pixl} \) (a conversion factor specifying the world space equivalent for each pixel in the texture), and \( S_{streak} \) (an artist-controlled scale factor to give different lengths of streaks to different types and intensities of rain, e.g., light rain has longer streaks than heavy rain).

```
\( E = \frac{S_{streak}}{S_f * (C_{pixl} * S_f * Vec_{precip} + S_{streak})} \) (5.2.2)
```

# Rendering Snow or Rain in Parallax

In addition to providing the sense of particles moving past the player, we want to provide a sense of depth and parallax. Raindrops or snowflakes in the distance should look smaller and fall slower than ones close by [Langer03]. To simulate this, we apply our texture scrolling technique to multiple textures. Our system used four textures, scaling down the texture coordinates progressively on each one to produce smaller precipitation drops and slower scrolling. We use Direct3D fixed function multitexturing to blend the four textures together.

The amount of scaling down depends on the type and intensity of precipitation, and is controlled by our artists.

Although this produces the parallax effect, the \( Z \) information is incorrect. The textures are designed to look far from the camera, but they are actually rendered on a plane at a close distance. When the drops are small enough, however, this is not a noticeable artifact.

# Simulating Camera Movement with a Cone

When the camera is traveling forward, the rain or snow should tilt so that it appears to be shooting at and past the camera. Similarly, when the camera moves sideways, the precipitation streaks are expected to have a sideways component to their motion. To simulate these effects, we map the four precipitation textures onto a double cone, as shown in Figure 5.2.4. Our textures are designed to tile so that no seams are visible when they are repeated across the cone surface, or as they scroll across the cone.

To reduce the visibility of the singularities at the cones' tips, we make the cones more transparent at those points, gradually fading in toward the circle at which the cones meet. We also select an appropriate cone height to tune the angle at which the rain appears to fall. If the cone is too short, when the camera is stationary, the rain will fall at an unrealistic slanted angle rather than straight down due to the cone's steep edges. On the other hand, the cone must not be too tall. This ensures that when the camera is moving and the cone is rotated, the rain will fall from the middle of the screen toward the edges as desired.