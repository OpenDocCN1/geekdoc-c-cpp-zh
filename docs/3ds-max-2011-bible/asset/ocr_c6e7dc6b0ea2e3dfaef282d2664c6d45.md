# ## Accessing mental ray materials and shaders

With the mental ray (or Quicksilver) renderer selected, all non–mental ray materials include an additional rollout labeled mental ray Connection. This rollout, shown in Figure 30.8, is available only if the mental ray extensions are enabled in the mental ray panel of the Preference Settings dialog box. They let you override the existing shaders used by the Scanline renderer and enable additional shaders that the mental ray renderer supports.

![](bbox=[0.013, 0.288, 0.306, 0.508])

The mental ray Connection rollout in the Material Editor lets you override the default shaders.

The lock icons to the right of the shader buttons are the default shaders used by the Scanline renderer. To select a new shader, simply unlock these shaders by clicking the shader buttons. If a material is opaque, you can speed up the rendering process by flagging the material as Opaque, using the option at the bottom of the rollout.

If you want to get direct access to the shaders used by mental ray, use the mental ray material type, which presents all the shaders listed in the mental ray Connection rollout.

# ## Using the Autodesk Material Library and the Arch & Design materials

The Autodesk Material Library and the Arch & Design materials are a set of advanced mental ray materials designed for architects to add to buildings and surfaces found in architecture renderings. All of these materials are based on physical properties that are typically found in environments lighted with global illumination. For example, the Satin Varnished Wood template includes slightly blurred reflections and a high glossiness to give it a realistic look.

The materials contained in the Autodesk Material Library are categorized into groups and subgroups. Each material has several parameters allowing you to change the color, glossiness, reflectivity, and so on. The available parameters change based on the selected material.

Many of the Arch & Design materials are already defined and available in the Templates rollout. The available presets include Pearl Finish, Satin Varnished Wood, Glazed Ceramic, Glossy Plastic, Masonry, Leather, Frosted Glass, Translucent Plastic Film, Brushed Metal, and Patterned Copper.