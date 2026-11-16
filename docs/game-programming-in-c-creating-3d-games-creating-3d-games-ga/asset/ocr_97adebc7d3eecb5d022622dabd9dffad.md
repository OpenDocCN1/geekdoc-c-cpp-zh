greener. Adding the output color to the existing color doesn't require any changes to the fragment shader code itself; instead, you can do this on the C++ side of things.

# Drawing Point Lights

You need to add some glue code to Renderer and PointLightComponent before you can draw the point lights in DrawFromGBuffer. First, you add a new shader member variable called mGPointLightShader. You then load this shader in LoadShaders. For the vertex shader, you use the BasicMesh.vert shader from Chapter 6 because the point light's sphere mesh doesn't need any special behavior. For the fragment shader, you use the GBufferPointLight.frag shader.

As with the global lighting shader, you need to set the uniforms for the different samplers to bind them to specific G-buffer textures. You also set the uScreenDimensions uniform to the width and height of the screen.

You also add a mPointLightMesh member variable that simply points to the mesh you want to use for the point lights. You load the mesh when initializing the Renderer and save it in the variable; the mesh in question is a sphere.

Now you add additional code to DrawFromGBuffer, shown in Listing 13.14. This code goes after all the code that drew the full-screen quad that applied global