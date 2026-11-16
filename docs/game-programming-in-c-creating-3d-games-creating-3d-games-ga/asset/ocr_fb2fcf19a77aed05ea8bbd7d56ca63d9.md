# # Loading Shaders

Once you have the separate shader files written, you must load in these shaders in the game's C++ code to let OpenGL know about them. At a high level, you need to follow these steps:

+   1. Load and compile the vertex shader.
+   2. Load and compile the fragment shader.
+   3. Link the two shaders together into a “shader program.”

There are many steps to loading a shader, so it is a good idea to declare a separate Shader class, as in Listing 5.5.

# ## Listing 5.5 Initial Shader Declaration

Click here to view code image

```
class Shader
{
public:
    Shader();
    ~Shader();

    // Load the vertex/fragment shaders with the giver
    bool Load(const std::string& vertName,
              const std::string& fragName);

    // Set this as the active shader program
```