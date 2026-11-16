```
yScale = cot( fov / 2 )
xScale = yScale . height / width
Perspective = [ xScale 0 0 0 ; 0 yScale 0 0 ; 0 0 far/(far-near) 1 ; 0 0 -near*far/(far-near) 0 ]
```

```
yScale = cot( fov / 2 )
xScale = yScale . height / width
Perspective = [ xScale 0 0 0 ; 0 yScale 0 0 ; 0 0 far/(far-near) 1 ; 0 0 -near*far/(far-near) 0 ]
```

Note that the perspective matrix changes the w component of the homogeneous coordinate. The **perspective divide** divides each component of the transformed vertex by the w component, so that the w component becomes 1 again. This is what reduces the size of objects as they get farther from the camera. OpenGL automatically does a perspective divide behind the scenes.

note
We omit the derivation of the orthographic and perspective matrices here.