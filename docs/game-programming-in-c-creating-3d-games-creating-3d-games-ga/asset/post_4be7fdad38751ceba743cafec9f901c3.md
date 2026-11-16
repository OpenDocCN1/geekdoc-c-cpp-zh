
```cpp
// Set sprite shader and vertex array objects active
mSpriteShader->SetActive();
mSpriteVerts->SetActive();

// Draw all sprites
for (auto sprite : mSprites)
{
    sprite->Draw(mSpriteShader);
}

// Swap the buffers
SDL_GL_SwapWindow(mWindow);
return true;
}
```

What happens when you run this code now? Well, first, the fragment shader only writes out a blue color. So it's reasonable to expect that you'd see blue squares for each SpriteComponent. However, there's another issue: For every sprite, you use the same sprite verts. These sprite verts define a unit square in normalized device coordinates. This means that for every `SpriteComponent`, you merely draw the same unit square in NDC. Thus, if you run the game right now, you'll see only a gray background and a rectangle, as in Figure 5.3.

![](img/e9afcec1487716b0ef80d7e7c09869c8_347_0.png)

Figure 5.3 Drawing many NDC unit squares (even though it looks like one rectangle)

It may seem like the solution is to define different vertex arrays for each sprite. However, it turns out that with only this one vertex array, you can draw whichever sprites you want to. The key is to take advantage the vertex shader's ability to transform vertex attributes.

## TRANSFORMATION BASICS

Suppose a game has 10 asteroids moving around. You could represent these 10 asteroids individually with different vertex array objects. However, you need these asteroids to show up in different locations onscreen. This means the triangles you draw for each asteroid need different normalized device coordinates.

A naïve idea is to create 10 different vertex buffers, 1 for each of the 10 asteroids, and recompute the vertex positions in these vertex buffers as needed. But this is wasteful both in terms of memory usage and in terms of computation. Changing vertices in vertex buffers and resubmitting them to OpenGL is not efficient.

Instead, think of a sprite in an abstract sense. Every sprite is ultimately just a rectangle. Different sprites may have different locations on the screen, different sizes, or different rotations, but they're still rectangles.

Thinking of it this way, a more efficient solution is to have a single vertex buffer for the rectangle and just reuse it. Every time you draw the rectangle, you may have a position offset, scale, or rotation. But given the NDC unit square, you can change, or **transform**, it such that it is an arbitrary rectangle with an arbitrary position, scale, and/or orientation.

This same concept of reusing a single vertex buffer for a type of object also extends to 3D. For example, a game taking place in the forest might have hundreds of trees, many of which are only slight variations of each other. It's inefficient to have a separate vertex buffer for every single instance of the same tree. Instead, you could create a single tree vertex buffer, and the game could draw many instances of this same tree with some variation in position, scale, and orientation.

### Object Space

When you create a 3D object (such as in a 3D modeling program), you generally don't express vertex positions in normalized device coordinates. Instead, the positions are relative to an arbitrary origin of the object itself. This origin is often in the center of the object, but it does not have to be. This coordinate space relative to the object itself is object space, or model space.

As discussed earlier in this chapter, defining a coordinate space requires knowing both the origin of the coordinate space and the direction in which the various components increase (the basis vectors). For example, some 3D modeling programs use +y as up, whereas others use +z as up. These different basis vectors define different object spaces for the objects. Figure 5.4 illustrates a 2D square where the center of the square is its object space origin, +y moves up, and +x moves right.

![](img/e9afcec1487716b0ef80d7e7c09869c8_350_0.png)

Figure 5.4 A quad relative to its object space origin

Now imagine a game that takes place in an office building. You'd need models for computer monitors, keyboards, desks, office chairs, and so on. You'd create each of these individual models in its own object space, which means each object's vertex positions are relative to that model's unique object space origin.

At runtime, you load each unique model into its own vertex array object (VAO). For example, you might have a VAO for the monitor, one for the keyboard, and so on. When it's time to render the scene, each vertex of each object you draw goes to the vertex shader. If you just directly passed along the vertex positions, as in `Basic.vert`, then you're saying that these vertex positions are in normalized device coordinates.

This is a problem because the coordinates for the models are not in NDC but instead are relative to each object's unique object space. Passing through the vertex positions as is would yield garbage output.

### World Space

To solve the problem with different objects having different object space coordinates, you first define a coordinate space for the game world itself. This coordinate space, called **world space**, has its own origin and basis vectors. For the game in the office building, the origin of world space might be in the center of the building on the ground floor.

Much as an office planner might place the desks and chairs at different positions and orientations in the office, you can think of the objects in the game as having arbitrary positions, scales, or orientations relative to the world space origin. For example, if there are five instances of the same desk placed in the office, each of these instances needs information describing how the object appears in world space.

When you draw each instance of the desk, you use the same vertex array object for each desk. However, each instance now needs some additional information, specifying how you want to *transform* the object space coordinates into world space. You can send this extra data to the vertex shader when drawing an instance, which allows the vertex shader to adjust the vertex positions as needed. Of course, the graphics hardware ultimately needs the coordinates in NDC to draw them, so you still have an additional step after transforming the vertices into world space. For now, let's look at how to transform vertices from their object space into world space.

### Transforming to World Space

When transforming between coordinate spaces, you need to know whether the basis vectors between the two coordinate spaces are the same. For example, consider the point (0, 5) in object space. If you define object space with +y as up, this means that the point (0, 5) is five units “above” the origin. However, if you choose to define world space such that +y is to the right, (0, 5) is instead five units to the right.

For now, assume that the basis vectors in object and world space are the same. Because the game currently is 2D, you can assume that +y is up and +x is to the right for both object space and world space.

> note
> The 2D coordinate system used here is different from the SDL coordinate system where +y is down! This means the code for Actor::GetForward no longer negates the y component. Furthermore, if you use atan2 for any calculations, you no longer negate the first parameter.

Now consider a unit square centered around the object space origin, as in Figure 5.4. Assume that the world space origin is the center of the game window. The goal is to take the unit square centered around its object space origin and express it as a rectangle with an arbitrary position, scale, or orientation relative to the world space origin.

For example, suppose one instance of the rectangle should appear in world space such that it's double in size and is 50 units to the right of the world space origin. You can accomplish this by applying mathematical operations to each vertex of the rectangle.

One approach is to use algebra equations to compute the correct vertex positions. Although you ultimately won't approach it in this manner, this is a useful bridge to understanding the preferred solution. This chapter focuses on 2D coordinate systems, though the same method outlined here would also work in 3D (just with an additional z component).

### Translation

Translation takes a point and translates, or moves, it by an offset. Given the point (x, y), you can translate it by the offset (a, b) by using the following equations:

```
x' = x + a
y' = y + b
```

For example, you could translate the point (1, 3) by the offset (20, 15) as follows:

```
x' = 1 + 20 = 21
y' = 3 + 15 = 18
```

If you apply the same translation to every vertex of a triangle, you translate the entire triangle.

### Scale
