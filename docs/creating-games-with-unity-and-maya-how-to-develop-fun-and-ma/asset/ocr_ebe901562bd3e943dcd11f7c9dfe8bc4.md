# Plan of Attack

As implied in this chapter, the main focus will be on baking the lighting of the scene. This will actually take a few steps that build upon each other. First, before we start doing much lighting, we will look at some advanced shader construction—the use of Normal Maps, which will help to provide surfaces that appear bumpy (or not) and not just like flat objects with color on them. This advanced shader construction will come in handy as we look at Unity's lighting scheme and how to control Unity's lighting instruments.

Finally, once some real-time lighting has been established we will look at baking strategies and settings to get a nicely baked lightmap that will look good in the game. Along the way, we will light the scene for a couple of different scenarios—first for a bright sunny day (since it allows the effects of light maps to be seen most clearly), and then for the dark, damp, and dismal day that the game actually calls for.

# Tutorial 7.1: Normal Maps

**Normal maps** are maps that help create more tactile-looking surfaces. Normal maps don't actually change the polygons of a surface—they don't really change the object they are attached to, but they present the visible representation of a more complex form. The grandfather of normal maps was bump maps, but normal maps are more powerful in some important ways.

Bump maps were largely grayscale (or at least that was the only value that mattered to the 3D software rendering them). When the texture map that was used to define bump had pixels closer to white, they were rendered as raised and pixels close to black were rendered as receding. The power of this was that a surface looked as though it had all sorts of bumps and valleys when the geometry did not.

Normal maps take this to the next level in that they use a similar idea, but instead of simply rendering the surface as raised or lowered in one direction, they describe the x, y, and z coordinates of a normal vector. The science and math here is well beyond what is relevant, but the net results are low-poly forms that are able to visually indicate much higher forms. The textures react to change in light and behave in believable and predictable ways as a player moves around them. In 3D arenas where polycount is important (like games), normal maps are tremendously powerful.

Historically, there are three ways that normal maps are usually created. The first is to actually model a very high-poly version of a surface (including characters) and then generate a normal map from that high-poly mesh that will be applied to a much lower-rez version of the form. In many ways this is most accurate, and frankly often produces the best normal maps. However,