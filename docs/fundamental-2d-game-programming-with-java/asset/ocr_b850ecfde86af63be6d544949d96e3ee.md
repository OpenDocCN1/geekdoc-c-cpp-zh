# CALCULATING A REFLECTION VECTOR

Once an intersection point is found, a reflection vector can be calculated. This vector is the direction the object would bounce off the line segment. See Figure 15.21.

![](bbox=[0.1, 0.17, 0.55, 0.33])

Figure 15.21 Reflection Vector. © 2014 Timothy Wright.

The intersection point can be found with a line intersection test. All that is needed to calculate the reflection vector is the original vector and a perpendicular vector to the reflection segment. The reflection vector is calculated as follows:

As shown in Figure 15.22, the vector V is the original direction vector. It is reflected off of the line segment AB. The normal is a normalized vector perpendicular to the AB line segment.

![](bbox=[0.1, 0.58, 0.65, 0.78])

Figure 15.22 Reflection Vector Proof. © 2014 Timothy Wright.