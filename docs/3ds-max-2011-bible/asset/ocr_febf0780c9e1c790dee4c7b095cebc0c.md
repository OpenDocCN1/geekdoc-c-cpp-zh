# Part IV: Materials, Cameras, and Lighting Basics

# FIGURE 16.7

Materials with the Anisotropic shader applied have elliptical highlights.

![](bbox=[0.069, 0.17, 0.6, 0.247])

# Tip

The Multi-Layer shader is useful to give a material a sense of surface depth. For example, it can give the illusion of a layer of shellac on wood or a layer of wax on tile.

# FIGURE 16.8

Materials with a Multi-Layer shader applied can have two crossing highlights.

![](bbox=[0.069, 0.419, 0.6, 0.497])

# Oren-Nayar-Blinn shader

The Oren-Nayar-Blinn shader is useful for creating materials for matte surfaces such as cloth and fabric. The parameters are identical to the Blinn shader, with the addition of the Diffuse Level and Roughness values.

# Metal shader

The Metal shader simulates the luster of metallic surfaces. The Highlight curve has a shape that is different from that of the other shaders. It is rounder at the top and doesn’t include a flat senvue. It can also accept a much higher Specular Level value (up to 999) than the other shaders. Also, you cannot specify a Specular color. All other parameters are similar to those of the Blinn shader. Figure 16.9 shows several materials with the Metal shader applied. These materials differ in Specular Level values, which are (from left to right) 50, 100, 200, 400, and 800.

# Note

For the Metal shader, the specular color is always the same as the material’s diffuse color.

# Strauss shader

The Strauss shader provides another alternative for creating metal materials. This shader has only four parameters: Color, Glossiness, Metalness, and Opacity. Glossiness controls the entire highlight shape. The Metalness value makes the material appear more metal-like by affecting the primary and secondary highlights. Both of these values can range between 0 and 100.