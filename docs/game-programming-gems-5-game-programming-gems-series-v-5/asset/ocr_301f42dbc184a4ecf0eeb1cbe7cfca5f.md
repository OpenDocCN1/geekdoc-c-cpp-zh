The sphere is the first of the volume emitters we will cover. Unlike lines or boxes, there is pretty much only one way to represent a sphere, and that’s with an origin and a radius (Table 7.3.6). As explained in the “Method” section, the volume emitters have a special function that occurs when the listener is inside them—the sound is played at full volume in all directions. There is no special case math required for this, as both the sphere’s and the box’s closest-point equations take this into account automatically.

Using a sphere for a sound effect like a small explosion will not give you much benefit. In fact, most sphere emitters can be replaced by a point emitter without the player noticing the difference. The spheres become useful only when there is a visual representation of the sound to go with the sphere, and it’s only that the player can walk into and out of. Note that the boxes do not suffer from this, as they change the way the sound moves (along a single axis as opposed to spherically, like the points and spheres), and therefore can’t be replaced by any other emitter.

The closest-point equation for a sphere is provided in Equation 7.3.4.

```
V = X - S_origin
d = min(|V|, S_radius)
A = S_origin + V_hat d
(7.3.4)
```

It is created with the following steps:

+   1. Create a vector between the listener and the center of the sphere.
+   2. Take the smallest value between the magnitude of this vector and the radius of the sphere. This will be how far away from the sphere’s origin to place the sound source. If the listener is inside the sphere, the magnitude will be the smallest, otherwise, it’ll be the radius.
+   3. Calculate the source position by scaling the normalized vector by the distance and adding it to the sphere’s position. This point will be on the surface of the sphere if the listener is outside, otherwise, it will be at the same place as the listener.

# Uses

Some possible uses include the following:

+   **Explosions:** Although most small explosions are best represented with a point primitive; if the explosion has an expanding radius, the sphere emitter would be the best option. It would be even better if you could tie in the radius of the emitter with the radius of the shockwave on screen.
+   
+   **Shields:** When surrounded by a shield, the noise will appear to surround you. To those outside, it will be generated on the surface. The bigger the shield, the more obvious the effect. If the players can walk into and out of the shield, it is another way of letting them know that they’re inside it.