
# Chapter 22: Animating with Constraints and Simple Controllers

## FIGURE 22.10

The Linear controller uses straight lines.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_656_0.png)

### Noise controller

The Noise controller applies random variations in a track's values. In the Noise Controller dialog box, shown in Figure 22.11, the Seed value determines the randomness of the noise and the Frequency value determines how jagged the noise is. You also can set the Strength along each axis. The > 0 option for each axis makes the noise values remain positive.

## FIGURE 22.11

The Noise controller properties let you set the noise strength for each axis.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_656_1.png)

You also have an option to enable Fractal Noise with a Roughness setting.

The Ramp in and Ramp out values determine the length of time before or until the noise can reach full value. The Characteristic Graph gives a visual look at the noise over the range. Figure 22.12 shows the Noise controller assigned to the Position track. If you need to change any Noise properties, right-click the Noise track and select Properties from the pop-up menu.

### Spring controller

The Spring controller is similar in many ways to the Flex modifier in that it adds secondary motion associated with the wiggle of a spring after a force has been applied and then removed. When the Spring controller is applied, a panel with two rollouts appears. These rollouts, shown in Figure 22.13, let you control the physical properties of the spring and the forces that influence it.

## Part V: Animation and Rendering Basics

## FIGURE 22.12

The Noise controller lets you randomly alter track values.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_657_0.png)

## FIGURE 22.13

The Spring controller rollouts can add additional springs and forces.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_657_1.png)

In the Spring Dynamics rollout, you can change the Mass and Drag values. Higher mass values result in greater secondary motion as the object is moved, and the Drag value controls how quickly the bouncing motion stops. You can add multiple springs, each with its own Tension and Damping values to be applied Relative or Absolute.

# Chapter 22: Animating with Constraints and Simple Controllers

The Forces, Limits, and Precision rollout lets you add forces that affect the spring motion. The Add button lets you identify these forces, which are typically Space Warps, and you can limit the effect to specific axes.

### Tutorial: Wagging a tail with the Spring controller

One of the best uses of the Spring controller is to gain the secondary motion associated with an existing motion. For example, if a character moves, then an appendage such as a tail can easily follow if you apply a Spring controller to it.

To wag a row of spheres using the Spring controller, follow these steps:

- 1. Open the Dog wagging tail.max file from the Chap 22 directory on the DVD. This file contains a linked row of spheres with the head sphere animated rotating back and forth.
- 2. Select the smallest sphere, and choose the Animation ▸ Position Controllers ▸ Spring menu command. This moves the sphere to its parent. Choose the Select and Move button (or press the W key), and return the sphere to its original position.
- 3. Repeat Step 2 for the remaining spheres, moving from smallest to largest.
- 4. Click the Play Animation button (or press the / key) to see the resulting motion.

Figure 22.14 shows a frame of the final motion. Notice that the spheres aren't lined up exactly. The smallest sphere is moving the greatest distance because all the springs are adding their effect.

## FIGURE 22.14

The Spring controller adds secondary motion to the existing motion of the largest sphere.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_658_0.png)

### Position XYZ controller

The Position XYZ controller splits position transforms into three separate tracks, one for each axis. Each axis has a Bézier controller applied to it, but each component track can be assigned a different controller. The Position XYZ Parameters rollout lets you switch between the component axes.

The Rotation tracks use a variety of controllers, many of them common to the Position track. This section lists the controllers that can be used only with the Rotation track.

### Scale XYZ controller

Max has one controller that you can use only in Scale tracks. The Scale XYZ controller breaks scale transforms into three separate tracks, one for each axis. This feature enables you to precisely control the scaling of an object along separate axes. It is a better alternative to using Select and Non-Uniform Scale from the main toolbar because it is independent of the object geometry.

The Scale XYZ Parameters rollout lets you select which axis to work with. This controller works the same way as the other position and rotation XYZ controllers.

## Summary

Using the Animation > Constraints menu, you can apply constraints to objects. This menu also lets you select a target object. You can use the various constraints to limit the motion of objects, which is helpful as you begin to animate. If you're an animator, you should thank your lucky stars for controllers. Controllers offer power flexibility for animating objects—and just think of all those keys that you don't have to set by hand.

This chapter covered the basics of using the Expression controller. Using mathematical formulas to control the animation of an object's transformation and parameters offers lots of power. You also can use the values of one object to control another object.

In this chapter, you accomplished the following:

- Constrained an object to the surface of another object using the Attachment and Surface constraints
- Forced an object to travel along a path with the Path constraint
- Controlled the position and orientation of objects with weighted Position and Orientation constraints
- Shifted between two different controlling objects using the Link constraint
- Followed objects with the LookAt constraint
- Learned about the various controller types
- Discovered how to assign controllers using the Motion panel and the Track View
- Saw a few examples of using controllers

In the next chapter, you learn to final render a scene so you can have some output to hang on Mom's fridge.

# Rendering a Scene and Enabling Quicksilver

After hours of long, hard work, the next step—rendering—is where the rubber hits the road and you get to see what you’ve worked on so hard. After modeling, applying materials, and positioning lights and cameras, and animating your scene, you’re finally ready to render the final output. Rendering deals with outputting the objects that make up a scene at various levels of detail.

Max includes a Scanline Renderer that is optimized to speed up this process, and several settings exist that you can use to make this process even faster. Understanding the Render Scene dialog box and its functions can save you many headaches and computer cycles. However, other rendering options are available.

The need for all these different rendering engines comes about because of a trade-off between speed and quality. For example, the renderer used to display objects in the viewports is optimized for speed, but the renderer used to output final images leans toward quality. Each renderer includes many settings that you can use to speed the rendering process or improve the quality of the results.

## Render Parameters

Commands and settings for rendering an image are contained within the Render Scene dialog box. This dialog box includes several tabbed panels.

After you’re comfortable with the scene file and you’re ready to render a file, you need to open the Render Scene dialog box, shown in Figure 23.1, by means of the Rendering ▸ Render Setup menu command (F10) or by clicking the Render Scene button on the main toolbar. This dialog box has several panels: Common, Renderer, Render Elements, Raytracer, and Advanced Lighting. The Common panel includes commands that are common for all renderers, but the Renderer panel includes specific settings for the selected renderer.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_660_0.png)

**IN THIS CHAPTER**

- Setting render parameters and preferences
- Using the Rendered Frame Window
- Working with the ActiveShade window and the RAM Player
- Understanding render types
- Creating an environment
