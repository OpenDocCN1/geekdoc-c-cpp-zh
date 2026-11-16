game, this type of view-projection matrix is insufficient. Instead, you need to decompose the view-projection matrix into separate view and projection matrices.

# View Matrix

The view matrix represents the position and orientation of the camera, or “eye” in the world. Chapter 9, “Cameras,” covers several different implementations of cameras, but for now let’s keep it simple. At a minimum, a look-at matrix represents the position and orientation of the camera.

In the typical construction of a look-at matrix, there are three parameters: the position of the eye, the target position the eye “looks at,” and the up direction. Given these parameters, you first compute four different vectors:

```
$$\hat{k} = \frac{target - eye}{\|target - eye\|}

\hat{i} = \frac{up \times \hat{k}}{\|up \times \hat{k}\|}

\hat{j} = \frac{\hat{k} \times \hat{i}}{\|\hat{k} \times \hat{i}\|}

\vec{t} = \langle -\hat{i} \cdot eye, -\hat{j} \cdot eye, -\hat{k} \cdot eye \rangle$$
```