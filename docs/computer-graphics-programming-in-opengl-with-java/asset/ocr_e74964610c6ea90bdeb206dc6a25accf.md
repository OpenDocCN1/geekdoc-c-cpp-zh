```
```glsl
layout(binding=0) uniform sampler3D s;
void main(void)
{ fragColor = texture(s, vec3(tc.x, tc.y, 0));    // gradually-changing "d" replaces previous constant
}
```
```

The full implementation on the accompanying CD includes a few additional minor changes to the turbulence() function to enhance the drifting cloud effect. While we cannot show the effect of gradually changing drifting and animated clouds in a single still image, Figure 14.23 shows such changes in a series of snapshots of the 3D generated clouds as they drift across the sky dome from right to left and slowly change shape while drifting.

![](bbox=[0.3, 0.345, 0.73, 0.88])

**Figure 14.23**
3D clouds changing while drifting.