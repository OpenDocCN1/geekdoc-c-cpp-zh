# Making Noise

The basic idea behind cloud rendering is to generate and animate noise over time to make the clouds change shape in a plausible way. As we want to perform all our computations on the GPU, current implementations of 3D Perlin Noise aren’t well suited for our task. Instead, we will composite multiple precomputed noise textures at different octaves and weights. Each composite of noise adds detail to the final texture—the first octave gives the rough shape, and the more octaves we use, the more details we add. We have found that using eight octaves of noise is a good trade-off between performance and visual quality.

# Octave Compositions

Each noise octave is represented by a smoothed 128 × 128 noise texture. This noise is generated with random numbers, and smoothing is performed with simple neighborhood filtering. Because the noise is signed, you may have to perform some scaling and biasing to pack the data into the textures and when you sample from them in your pixel shaders, depending on the texture format you’re using. In our pixel shader, all eight octaves are added together with different scales and weights to achieve the desired effect. That is, the first octave is not tiled, giving the rough shape of the final composite noise. As we continue to add in higher octaves, they are repeated more frequently and weighted less, giving more and more fine detail, as shown in Figure 5.1.2. Playing with the tiling rates and weight factors allows you to tune the look of your clouds. Giving more weight to higher octaves results in smaller cloud formations, but still provides the rough shape defined by the lower octaves. Good starting values are 1, 2, 4, 8, and so on for octave scales, and 1, 1/2, 1/4, 1/8, and so on for octave weights.

# Animating the Noise

Animating the noise texture is simply a matter of animating the octave textures over time, as discussed in [Elias] and [Pallister01]. Low octaves should animate more slowly than high octaves. This way, the basic shape of our clouds will change slowly, while finer details will change faster. For each octave, we keep two noise textures and interpolate slowly between them at different rates. We will return to this step later when we discuss optimizations.

# Cloud Density

So far, we have created our basic building block: dynamic noise with controllable octaves. A typical image of eight octaves of noise is shown in Figure 5.1.3a. We must now perform a few more steps to make this noise appear more cloudlike. For example, we need to be able to control the percentage of clouds in the sky. To do this, we sub-