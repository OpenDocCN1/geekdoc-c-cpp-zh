# Tutorial: Throwing a shirt over a chair

In the preceding example, you looked at something that reactor made much easier, but in this example, you see some animations that would be impossible without reactor. Cloth deformation is very difficult to animate, but it is much easier if you correctly apply the laws of physics to describe this motion. In this simple example, you throw a stiff shirt over a stationary chair to see how it reacts.

To animate cloth falling over a hard object, follow these steps:

+   1. Open the Shirt over chair.max file from the Chap 43 directory on the DVD. This file includes a chair object and a shirt that is nothing more than an extruded shape that has been sufficiently subdivided.
+   2. Select Animation ▸ reactor ▸ Create Object ▸ Rigid Body Collection, and click in the Front viewport to create the collection icon. Click the Add button, and select the chair and the floor objects to add them both to the Rigid Body Collection.
+   3. Select the chair and floor object, and choose Animation ▸ reactor ▸ Open Property Editor. Select the Unyielding option. Then right-click to exit Rigid Body Collector mode.
+   4. Select the shirt object, and choose Animation ▸ reactor ▸ Apply Modifier ▸ Cloth Modifier.
+   5. With the shirt object still selected, choose Animation ▸ reactor ▸ Create Object ▸ Cloth Collection to create a Cloth collection that contains the shirt object.
+   6. Now preview the animation before computing it. Select Animation ▸ reactor ▸ Preview Animation to open the Preview window, and press the P button. When the animation finishes (and the shirt falls on the chair), close the Preview window.
+   7. Select Animation ▸ reactor ▸ Create Animation to have the keys computed for this animation. Then click the Play button to see the final animation.

Figure 43.5 shows one frame of the finished animation.

![](bbox=[0.014, 0.625, 0.575, 0.939])