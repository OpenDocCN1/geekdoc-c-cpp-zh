# Using the Render Types

From the top of the Rendered Frame Window, the Area to Render drop-down list enables you to render subsections of the scene. The default setting is View. After you pick a selection from the list, click the Render button to begin the rendering. The available Render Types are described in Table 23.1.

# TABLE 23.1

# Render Type Options

| Render Type | Description |
|---|---|
| View | Renders the entire view as shown in the active viewport. |
| Selected | Renders only the selected objects in the active viewport. |
| Region | Places a frame of dotted lines with handles in the active viewport. This frame lets you define a region to render. You can resize the frame by dragging the handles. When you have defined the region, click OK in the lower-right corner of the active viewport. |
| Crop | Similar to Region in that it uses a frame to define a region, but the Crop setting doesn't include the areas outside the defined frame. |
| Blowup | Takes the defined region and increases its size to fill the render window. The frame for Blowup is constrained to the aspect ratio of the final resolution. |

At the top of the frame buffer window are several controls and icon buttons.

+   - The Edit Region button is activated when the Region option is selected. It lets you drag the center of the area to move it around or drag the edge and corner handles of the region to resize the render area. This option lets you precisely define the area that is rendered.
+   - The Auto Region Selected option automatically sets the render region to the current selection in the viewports.
+   - The Lock to Viewport causes all renders to be done using the specified viewport, regardless of which viewport is active. Using this option you can lock the renders to the Perspective viewport even if you're using a different viewport.
+   - The Render Setup button opens the Render Scene dialog box.
+   - The Environment and Effects Dialog button opens this dialog box, which includes the Exposure Control settings.
+   - The first is the Save Bitmap button, which enables you to save the current frame buffer image.
+   - The Copy Bitmap button copies the image in the Rendered Frame Window to the Windows clipboard where you can paste it into another application like Photoshop.
+   - The Clone Rendered Frame Window button creates another frame buffer dialog box. Any new rendering is rendered to this new dialog box, which is useful for comparing two images.
+   - The Print Image button sends the rendered image to the default printer.
+   - The Clear button erases the image from the window.