

segment, 与沿样条线上任意一点的方向来自控制点之间的插值。最后，每个控制点指定在单位沿线段移动时要播放的特定动画。控制点参数可以实时设置或由设计预先确定。重要的是选择“良好”的值。

## Choosing “Good” Prescribed Values

## 选择“良好”的预设值

For a prescribed physics system to work, it needs to look believable. For example, units should appear to fall realistically and bounce when they hit an obstacle. To sell the look of the system, it’s important that it has some of the same properties of a real simulation. The problem, then, is determining how to partially model the effects of a realistic system in the prescribed world.

要使预设物理系统正常工作，它需要看起来可信。例如，单位在撞到障碍物时应表现出真实的下落和反弹。为了让系统看起来可信，它需要具备真实模拟的一些相同属性。因此，问题在于如何在预设世界中部分模拟真实系统的效果。

Dynamics provides all the equations that are needed for a realistic simulation. Typically, an examination is made of the real-world equations that are necessary to model particular effects, such as gravity, buoyancy, drag, and friction. The equations are then combined, and some time points are chosen for motion and are plugged into the appropriate parameters. The equation is then solved for each time point, and the resulting table of time inputs and equation outputs can be fed right into the prescribed simulation. Note that increasing the granularity of the time points will increase the approximation of the real system.

动力学提供了真实模拟所需的所有方程。通常，会检查模拟特定效果（如重力、浮力、阻力和摩擦力）所需的现实世界方程。然后将这些方程组合，为运动选择一些时间点，并将其代入相应参数。然后针对每个时间点求解方程，得到的时间输入和方程输出表可以直接输入到预设模拟中。请注意，增加时间点的粒度将提高对真实系统的近似。

Another way to arrive at the input values for the prescribed system is to run a real simulation “offline” and record the position data over time. The “fake” simulation can then be made to match the real simulation data, resulting in a natural look and feel to the motion.

得到预设系统输入值的另一种方法是“离线”运行真实模拟并记录随时间变化的位置数据。然后可以让“假”模拟与真实模拟数据匹配，从而使运动看起来和感觉自然。

Once a prescribed physics system has been developed and a method for selecting values has been chosen, it’s easy to use the system to cover a variety of situations. What follows is a number of examples of prescribed physics applications.

一旦开发出预设物理系统并选择了值选择方法，就可以轻松使用该系统来覆盖各种情况。以下是预设物理应用的一些示例。

## Application: RTS Building Destruction

## 应用：RTS 建筑毁坏

In 3D RTS games, buildings generally build up out of the ground and fall back into the ground once they are destroyed. This simple behavior can easily be modeled using prescribed physics. A number of short spline segments are needed, positioned from the building’s center point to a point below the terrain, at a total distance sufficient to hide the top of the building under the terrain. Each control point’s quaternion contains a small pitch or roll amount, to simulate the building’s shaking. The speed of the control points should increase as they go down, so that the building appears to accelerate on its way to the ground. Figure 4.7.1 shows five control points for building destruction. In this example, five points are sufficient to show the varied speed and rotation for the destruction.

在3D即时战略游戏中，建筑物通常从地面升起，一旦被毁坏就会落回地下。这种简单的行为可以轻松使用预设物理来建模。需要若干短样条线段，从建筑物中心点定位到地形下方的一点，总距离足以将建筑物顶部隐藏在地形下。每个控制点的四元数包含少量俯仰或滚转量，以模拟建筑物的摇晃。控制点的速度在下降时应增加，以便建筑物看起来在下落过程中加速。图4.7.1显示了建筑物毁坏的五个控制点。在此示例中，五个点足以展示毁坏过程中的变化速度和旋转。

![](img/672fe9a2d008ba627b1991e15d70f43e_525_0.png)

图4.7.1 建筑物毁坏的样条线控制点。

## Application: Jumping

## 应用：跳跃

Jumping is another straightforward application for a prescribed physics system. From a stop, the unit runs a small distance, bends down, and leaps up. After a small amount of time, the unit comes down and lands. As shown in Figure 4.7.2, the unit should play a run animation and accelerate from control point A to B. At point B, the unit should play a “jump into the air” animation and begin with high velocity towards point C. The velocity should slow towards point D. While it is not possible to alter vertical and not horizontal velocity in this system, this simulation does not need such accuracy to look convincing. There is a slight pause in velocity about point D, at which point the acceleration due to gravity overcomes the unit’s upward velocity. The unit accelerates through point E and quickly arrives at point E. At point F, the unit plays a landing animation, which is accompanied by an appropriate visual effect for the terrain on which the unit lands. Point G completes the effect, allowing room for the unit to recover or stutter following the jump.

跳跃是预设物理系统的另一个直接应用。从静止开始，单位跑一小段距离，弯下腰，然后跳起。经过一小段时间后，单位落下并着陆。如图4.7.2所示，单位应播放跑步动画，并从控制点A加速到B。在B点，单位应播放“跳入空中”动画，并以高速向C点移动。速度应在向D点移动时减慢。虽然在此系统中无法改变垂直速度而不改变水平速度，但该模拟不需要如此精确即可看起来可信。在D点附近速度会有轻微停顿，此时重力加速度克服了单位的向上速度。单位通过E点加速并快速到达E点。在F点，单位播放着陆动画，并伴随单位着陆地形的适当视觉效果。G点完成效果，为单位在跳跃后恢复或踉跄留出空间。

![](img/672fe9a2d008ba627b1991e15d70f43e_525_1.png)

图4.7.2 跳跃效果的样条线控制点。

## Application: Explosion Displacement

## 应用：爆炸位移

Explosions are another great application for a prescribed physics system. As shown in Figure 4.7.3, units follow a somewhat parabolic spline. However, as opposed to actual physics, units will flip as they fly through the air. All units fly away from the center of the explosion. Units choose from a number of predetermined splines based on both their distance to the center of the explosion and some randomization factor. This, along with control point height and rotation randomization, provides for a lot of variety in the flight taken by units.

爆炸是预设物理系统的另一个绝佳应用。如图4.7.3所示，单位沿着某种抛物线样条线移动。然而，与实际物理不同，单位在空中飞行时会翻转。所有单位都从爆炸中心向外飞行。单位根据其到爆炸中心的距离和某些随机因素，从若干预设样条线中选择一种。这，加上控制点高度和旋转随机化，为单位的飞行提供了大量变化。

![](img/672fe9a2d008ba627b1991e15d70f43e_526_0.png)

图4.7.3 爆炸后沿抛物线路径移动的单位。© 2004。经Stainless Steel Studio许可转载。

Rotations are broken up over a few control points so that no single spline segment has too much rotation for its spline segment length. Breaking up the rotation also allows for the units to flip completely over. A unit should only rotate in one direction throughout the spline. While flips are a Hollywood effect, changing direction mid flight would be an obvious red flag to the player. At the end of the spline, any rotation must leave the unit on its back or on its stomach in preparation for the landing animation.

旋转被分散到几个控制点上，因此单个样条线段不会有过长的旋转角度。分解旋转还允许单位完全翻转。单位在整个样条线中应只向一个方向旋转。虽然翻转是好莱坞效果，但飞行中途改变方向会对玩家来说是一个明显的警示信号。在样条线末端，任何旋转都必须使单位仰面或俯卧着地，以准备着陆动画。

Animations are added to show the unit flying up off of the ground. Units can either fly forward on their stomach, or backward on their back. Once airborne, units play a mid-air flailing animation. For landing, “land-on-stomach” and “land-on-back” animations are used, as appropriate. The landing animation will sell the physics effect even better if it includes some amount of bounce for the unit on impact. Finally, an appropriate visual effect for the terrain collision should be added when the unit hits the ground, such as a dust cloud or tossing of other debris.

添加动画以显示单位从地面飞起。单位可以俯身向前飞行，或仰身向后飞行。一旦进入空中，单位会播放空中挣扎动画。对于着陆，根据情况使用“俯卧着陆”和“仰卧着陆”动画。如果着陆动画在撞击时包含单位的一定反弹，将更好地体现物理效果。最后，当单位撞到地面时，应添加适当的地形碰撞视觉效果，例如尘土云或其他碎片飞溅。

## Application: Buoyancy

## 应用：浮力

The effect for buoyancy is easy to simulate. What is really needed to convince a player of buoyancy? Units must fall to the water, at which point their descent is greatly reduced. After falling down through the water, the unit will stop, and then begin to rise. The unit rises faster and faster, until it breaks the surface of the water. Perhaps the unit breaks the water plane again on the way down and then resurfaces before coming to a resting position on top of the water. This is all that needs to be shown to sell the idea of buoyancy.

浮力效果易于模拟。要让玩家相信浮力，究竟需要什么？单位必须落入水中，此时其下降速度大大降低。在水中下落一段时间后，单位会停止，然后开始上升。单位上升速度越来越快，直到冲出水面。也许单位在下落过程中再次穿过水面，然后在停留在水面上之前再次浮出。这足以展示浮力的概念。

![](img/672fe9a2d008ba627b1991e15d70f43e_527_0.png)

图4.7.4 预设浮力效果的样条线控制点。

Figure 4.7.4 shows additional details of the buoyancy described. The speed between spline control points A and B should greatly reduce. This deceleration should continue to point C, at which point the buoyancy of the unit has overcome the force of gravity. The unit accelerates from a stop up to point D, with additional increases in speed to point E. From point E, the unit again accelerates from a stop. Points F and G repeat the process of gravity and buoyancy for the secondary splash-down but with greatly reduced time durations for each control point.

图4.7.4显示了所述浮力的更多细节。样条线控制点A和B之间的速度应大大降低。这种减速应持续到C点，此时单位的浮力已克服重力。单位从静止加速到D点，速度进一步增加到E点。从E点，单位再次从静止加速。F点和G点重复二次溅落的重力和浮力过程，但每个控制点的时间持续时间大大缩短。

To add realism, some animations are added. Units should use a tread water animation for points G and E, and a swim animation for points C, D, and F. Points A and B call for a falling animation. Each break of the water's surface should be accompanied by a visual splash effect. To add variety to the physics, a unit's density and mass should affect the depth of control points as well as the speed. Finally, should the unit have sufficient velocity, or if the water is shallow enough, the unit should kick off of the sea floor, and thus have an increased speed for points D and E.

为了增加真实感，添加了一些动画。单位在G点和E点应使用踩水动画，在C点、D点和F点应使用游泳动画。A点和B点需要下落动画。每次穿出水面都应伴随视觉溅起效果。为了增加物理变化，单位的密度和质量应影响控制点的深度以及速度。最后，如果单位具有足够速度，或者水足够浅，单位应从海底蹬起，从而使D点和E点的速度增加。

## Application: Paratroopers

## 应用：伞兵

For Empires: Dawn of the Modern World, some number of paratroopers were required to drop out of their C-47. The paratroopers needed to follow a realistic-looking path to the ground. Further, the paratroopers needed to land near the player-specified landing zone. Paratroopers were not allowed to land on illegal map locations, as this would frustrate players.

对于《帝国：现代世界的黎明》，需要若干伞兵从他们的C-47飞机上跳伞。伞兵需要沿着看起来真实的路径下降到地面。此外，伞兵需要在玩家指定的着陆区附近着陆。伞兵不允许在地图非法位置着陆，因为这会让玩家感到沮丧。

Each paratrooper had six spline control points created to move the paratrooper to its pre-calculated landing location. The positions of the spline control points were slightly randomized per paratrooper, creating unique flight paths for each. Further, subsequent splines would move the paratroopers in opposite directions, to further distribute their descent.

为每个伞兵创建了六个样条线控制点，以将伞兵移动到其预先计算的着陆位置。每个伞兵的样条线控制点位置都略有随机化，为每个伞兵创建独特的飞行路径。此外，后续样条线会将伞兵向相反方向移动，以进一步分散他们的下降。

Figure 4.7.5 (also Color Plate 4A) shows these six spline control points for one paratrooper. Control point 1 is the location from which the paratrooper begins his descent and is located on a tag point on the C-47 airplane model. As mentioned previously, control points 2, 3, and 4 are slightly random, so that subsequent paratroopers have varying flight paths. This variation is easier to see in Figure 4.7.6 (also Color Plate 4B), which provides a better perspective on the scene and features a whole stick of paratroopers. Control points 5 and 6 add a hook at the end of the spline. This hook ensures that the paratrooper intersects the terrain at the correct predetermined location. Note that control point 6 is actually below the terrain.

图4.7.5（另见彩色插图4A）显示了一个伞兵的这六个样条线控制点。控制点1是伞兵开始下降的位置，位于C-47飞机模型上的一个标记点上。如前所述，控制点2、3和4略有随机化，因此后续伞兵具有不同的飞行路径。这种变化在图4.7.6（另见彩色插图4B）中更容易看到，该图提供了场景的更好透视，并展示了一整排伞兵。控制点5和6在样条线末端添加了一个钩子。这个钩子确保伞兵在正确的预定位置与地形相交。请注意，控制点6实际上位于地形下方。

![](img/672fe9a2d008ba627b1991e15d70f43e_528_0.png)

图4.7.5 一个士兵的控制点。© 2004。经Stainless Steel Studios许可转载。

Each physics tick, the amount of time passed combined with the paratrooper's acceleration, was used to calculate the distance the paratrooper had traveled. Each spline segment had its length calculated before the simulation began. In this manner, the paratrooper could determine which segment of the spline it was currently following. Once the trooper knew its current spline segment, its new position along that

每个物理时钟周期，经过的时间量与伞兵的加速度结合，用于计算伞兵行进的距离。模拟开始前，每个样条线段的长度都已计算。这样一来，伞兵可以确定自己当前正在遵循样条线的哪个段落。一旦士兵知道了自己当前的样条线段，其沿该

