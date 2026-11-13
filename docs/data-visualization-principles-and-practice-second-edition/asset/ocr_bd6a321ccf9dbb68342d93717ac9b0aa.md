![](bbox=[0.07, 0.1, 0.79, 0.59])

Figure 11.25. Eight frames removed from a graph animation for visualizing a dynamic hierarchical call graph.

+   - If \( c_{edge}(e^i) = e^{i+1} \), i.e., \( e^i \) has a correspondence \( e^{i+1} \) in \( B^{i+1} \), we linearly interpolate \( e^i \) towards \( e^{i+1} \) as a function of the animation time \( t \), and color \( e^i \) blue.
+   - If \( c_{edge}(e^i) = \varnothing \), i.e., \( e^i \) has no correspondence in \( B^{i+1} \), we linearly interpolate the position of \( e^i \) towards a straight line linking its end points, color \( e^i \) green, and interpolate the opacity of \( e^i \) from 1 (fully opaque) towards 0 (fully transparent).
+   - If \( c(e^{i+1}) \neq e^i, \forall e^{i-1} \in E^{i-1} \), i.e., \( e^i \) has no correspondence in \( B^{i-1} \), we linearly interpolate from a straight line linking the end points of \( e^i \) towards the actual curve \( e^i \), color \( e^i \) red, and interpolate the opacity of \( e^i \) from 0 to 1.

The above procedure effectively creates a continuously changing bundle image \( B(t) \) that interpolates between the separate keyframe bundles \( B^i \). The final