posite transformations such as translation and rotation, or translation and scaling, or translation, rotation, and scaling.

# Rotation of a line

Problem Rotate a line with the coordinate point $L(x_1, y_1)$ and $L(x_2, y_2)$ around the origin by an angle $	heta$ to $L'(x_1, y_1)$ and $L'(x_2, y_2)$.

![](bbox=[0.167, 0.273, 0.715, 0.555])

# Method

Input the rotation angle.
Calculate the rotation matrix.

```
$R(\theta) = \begin{bmatrix} \cos\theta & -sin\theta & 0 \ \sin\theta & \cos\theta & 0 \ 0 & 0 & 1 \end{bmatrix}$
```

Where $R(\theta)$ is the rotation matrix and $	heta$ is the counterclockwise rotation angle of the line.

Input the coordinates of the line.

$L = (x_1, y_1) (x_2, y_2)$

Set up the coordinate matrix.