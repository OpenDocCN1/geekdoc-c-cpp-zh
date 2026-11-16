# Intense Fireball

The fireball is a secondary effect that kicks in after the first three effects. It starts at about 0.1 seconds after the start of the explosion and shoots outward from the center of the explosion. The fireball should start fully opaque and then fade out slowly after 0.3 seconds (as seen in the fourth column of Color Plate 8A).

As with the hot inner core, there are two ways that you can choose to render the fireball component of this explosion effect. The first method is the cheapest and involves a single particle. The second requires about 50 particles and is more expensive.

The cheap method uses a single texture shaped as an amorphous blob, similar to the cheap hot inner core step. The texture itself should be a mottled red fireball with black cloud-like edges within the texture, while the alpha channel should have a cloud-like density and amorphous shape. This particle will basically crossfade with the white hot inner core, scaling up at a similar rate with the exponential decay. After 0.3 seconds, the particle should slowly fade out.

The expensive method involves spawning roughly 50 particles in the center of the explosion. Each uses a texture similar to the cheap effect and each starts off very small and scales up slowly to a capped size. Each particle shoots from the center at a very high velocity in a random direction. The velocity will then exponentially decay until the particles are still, with only the combined wind and thermal buoyancy causing them to drift. Each particle should then fade out slowly after 0.3 seconds. To make the fireball more motile, it helps to darken particle vertex colors in particular octants of the explosion.

An important aspect of the expensive method is stretching of the fireball particles in the direction of motion. As each fireball particle moves away from the center, it relaxes into a square shape. This effect is very important in creating the feeling of power bursting from the center. Figure 5.6.4 shows how the billboard quad transforms over the particle's lifetime. Note that the particles become larger and more square as they expand outward and slow down.

![](bbox=[0.25, 0.68, 0.85, 0.85])

FIGURE 5.6.4 The transformation of the fireball billboard quad over its lifetime. Note how the quad starts out narrow in the direction of the explosion and then relaxes into a square shape.