# Chapter 45: Working with Advanced Lighting, Light Tracing, and Radiosity

# FIGURE 45.5

Use the Advanced Lighting panel in the Object Properties dialog box to disable advanced lighting.

![](bbox=[0.04, 0.25, 0.44, 0.72])

# Tutorial: Excluding Objects from Light Tracing

Using the Object Properties dialog box, you can exclude certain objects from the light tracing calculations.

To exclude objects from the Light Tracer, follow these steps:

+   1. Open the Hotplate.max file from the Chap 45 directory on the DVD.
+      This file includes a simple model of a hotplate.
+   2. Open the Advanced Lighting panel by selecting Rendering ⇨ Light Tracer (or press the 9 key). In the Parameters rollout, set the Bounces value to 2.
+   3. In the Front viewport, select the plug, cord, and floor objects, and then select Edit ⇨ Object Properties to open the Properties dialog box for these objects. In the Object Properties dialog box, open the Advanced Lighting panel and enable the Exclude from Advanced Lighting Calculations option. Then click OK.
+   4. In the Render Scene dialog box, click the Render button.
+      This renders the scene in the Rendered Frame Window.

Figure 45.6 shows the scene rendered with advanced lighting that excludes certain objects.