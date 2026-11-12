# Collision Handling

2D collisions are determined by the types of shapes colliding. For example, we have a rectangle-to-rectangle collisions or circle-to-circle collisions. In general, we would have a simple rectangular shape around the entity known as a "box collider". This technique is not perfect, but it offers a particularly good ratio between performance and function.

![](bbox=[0.14, 0.23, 0.84, 0.4])

Figure 36 Collision

A collision can be detected only when the two colliders are overlapping. This type of collision detection is not pixel perfect. What happens after the collision is up to us to decide.

We are going to create a collider component to make sure that only entities with a collider component can react to collisions. This is important because it will reduce the number of collision tests.

We are also going to create a separate system for collision handling to keep our code clean because it will make it easier for us later to add scripting features.

# Collider Component

The collider component should also be added to the header file physics.h. Following is a code snippet that shows the definition of the box collider component.

```
engine/src/ecs/components/physics.h
```