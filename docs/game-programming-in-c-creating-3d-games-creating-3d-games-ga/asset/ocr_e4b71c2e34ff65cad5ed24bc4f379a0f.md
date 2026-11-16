![](bbox=[0.25, 0.08, 0.6, 0.36])

Figure 5.4 A quad relative to its object space origin

Now imagine a game that takes place in an office building. You'd need models for computer monitors, keyboards, desks, office chairs, and so on. You'd create each of these individual models in its own object space, which means each object's vertex positions are relative to that model's unique object space origin.

At runtime, you load each unique model into its own vertex array object (VAO). For example, you might have a VAO for the monitor, one for the keyboard, and so on. When it's time to render the scene, each vertex of each object you draw goes to the vertex shader. If you just directly passed along the vertex positions, as in `Basic.vert`, then you're saying that these vertex positions are in normalized device coordinates.

This is a problem because the coordinates for the models are not in NDC but instead are relative to each object's unique object space. Passing through the vertex positions