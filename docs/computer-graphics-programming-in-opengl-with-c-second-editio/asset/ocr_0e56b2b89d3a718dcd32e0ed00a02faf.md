```
```cpp
float radius;        // sphere radius (only relevant if type=sphere)
vec3  mins;          // box corner (if type=box). If type=plane, X and Z values are width and depth
vec3  maxs;          // opposite box corner (if type=box)
float xrot;          // X component of object rotation (only relevant if type=box or plane)
float yrot;          // Y component of object rotation (only relevant if type=box or plane)
float zrot;          // Z component of object rotation (only relevant if type=box or plane)
vec3  position;      // location of center of object
bool  hasColor;      // whether or not the object has a particular color specified
bool  hasTexture;    // whether or not the object includes a texture image in computing its color
bool  isReflective;  // whether or not the object is reflective (generates a secondary ray)
                     // (if the object is a room box, this field is used to enable or disable lighting)
bool  isTransparent; // whether or not the object is refractive (generates a secondary ray)
vec3  color;         // the RGB color specified for the object (only relevant if hasColor is true)
float reflectivity;  // percentage of reflective color to include (only relevant if isReflective is true)
float refractivity;  // percentage of refractive color to include (only relevant if isTransparent)
float IOR;           // Index of Refraction (only relevant if isTransparent is true)
vec4  ambient;       // ADS ambient material characteristic
vec4  diffuse;       // ADS diffuse material characteristic
vec4  specular;      // ADS specular material characteristic
float shininess;     // ADS shininess material characteristic
};

Object[] objects =
{  // object #0 is the room box
   { 0, 0.0, vec3(-20, -20, -20), vec3( 20, 20, 20), 0, 0, 0, vec3(0), true, false, true, false, vec3(0.25,
     1.0, 1.0), 0, 0, vec4(0.2, 0.2, 0.2, 1.0), vec4(0.9, 0.9, 0.9, 1.0), vec4(1.0, 1.0, 1.0, 1.0), 50.0
   },
   // object #1 is the checkerboard ground plane
   { 3, 0.0, vec3(12, 0, 16), vec3(0), 0, 0, 0, vec3(0.0, -1.0, -2.0), false, true, false, false, vec3(0),
     0.0, 0.0, 0.0, vec4(0.2, 0.2, 0.2, 1.0), vec4(0.9, 0.9, 0.9, 1.0), vec4(1.0, 1.0, 1.0, 1.0), 50.0
   },
   // object #2 is the transparent sphere with slight reflection and no texture
   { 1, 1.2, vec3(0), vec3(0), 0, 0, 0, vec3(0.7, 0.2, 2.0), false, true, true, true, vec3(0),
     0.8, 0.8, 1.5, vec4(0.5, 0.5, 0.5, 1.0), vec4(1.0,1.0,1.0,1.0), vec4(1.0, 1.0, 1.0, 1.0), 50.0
   },
   // object #3 is the slightly reflective box with texture
   { 2, 0.0, vec3(-0.25, -0.8, -0.25), vec3(0.25, 0.8, 0.25), 0, 0, 70.0, 0.0, vec3(-0.75, -0.2, 3.4),
     false, true, true, false, vec3(0), 0.5, 0.0, 0.0, vec4(0.5, 0.5, 0.5, 1.0), vec4(1.0, 1.0, 1.0, 1.0),
     vec4(1.0, 1.0, 1.0, 1.0), 50.0
   }
};
int numObjects = 4;
...
vec3 getTextureColor(int index, vec2 tc)
```
```