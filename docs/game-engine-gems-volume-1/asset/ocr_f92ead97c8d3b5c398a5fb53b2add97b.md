# # 18.7 Results

The proposed methods have been implemented in DirectX/HLSL environment, and their performance has been measured on an Nvidia GeForce 8800 GTX GPU at 800×600 resolution. The rendering results of the harbor scene are shown in Figure 18.3. This scene can be rendered at 170 FPS if only directional light is computed. Taking 16 samples per pixel, the ambient occlusion and indirect lighting computation runs over 100 FPS. With 32 samples per pixel, the rendering speed drops to 60 FPS.

![](bbox=[0.16, 0.35, 0.59, 0.76])

**Figure 18.3:** (See also Color Plates.) Rendering results of the harbor scene— (First column) direct lighting, (second column) direct lighting plus ambient occlusion, and (third column) direct lighting plus ambient occlusion and indirect lighting.