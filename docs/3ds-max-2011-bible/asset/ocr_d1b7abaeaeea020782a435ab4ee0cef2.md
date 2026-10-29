The Advanced Lighting section offers options to use Advanced Lighting or Compute Advanced Lighting when Required. Advanced lighting can take a long time to compute, so these two options give you the ability to turn advanced lighting on or off.

# Cross-Ref

Advanced lighting is covered in more detail in Chapter 45, “Working with Advanced Lighting, Light Tracing, and Radiosity.”

# Bitmap Proxies

The Bitmap Proxies section includes a Setup button to enable a feature that can downscale all maps for the current scene. Clicking the Setup button opens the Global Settings and Defaults for Bitmap Proxies dialog box, shown in Figure 23.4.

# FIGURE 23.4

The Bitmap Proxies dialog box lets you replace all texture maps with proxy images.

![](bbox=[0.08, 0.64, 0.62, 0.81])

The Downscale map option lets you select to downscale all maps to Half, Third, Quarter, or Eighth, or to their current size. This lets you create your scene with high-quality maps and quickly reduce their sizes as needed without having to open and scale each individual map. The Proxy System lets you select to use a proxy image if the current map is larger than a specified size in pixels.

This dialog box also lets you set the Render Mode to be optimized for performance or memory. The options include Render with Proxies, Render with Full Resolution [image maps] In Memory, and Render with Full Resolution and Free up the Memory once Rendered.

# Choosing a Render Output option

The Render Output section enables you to output the image or animations to a file, a device, or the Rendered Frame Window. To save the output to a file, click the Files button and select a location in the Render Output File dialog box. Supported formats include AVI, BMP, DDS, Postscript (EPS), JPEG, Kodak Cineon (CIN), Open EXR, Radiance Image File (HDRI), QuickTime (MOV), PNG, RLA, RPF, SGI’s Format (RGB), Targa (TGA), and TIF. The Device button can output to a device such as a video recorder. If the Rendered Frame Window option is selected, then both the Files and Devices buttons are disabled. (The Rendered Frame Window is discussed later in this chapter.)