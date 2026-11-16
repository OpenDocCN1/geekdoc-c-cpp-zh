```
// Scalar product
Vector4D operator *(float s) const
{
 return (Vector4D(x * s, y * s, z * s, w * s));
}

// Dot product
float operator *(const Vector4D& v) const
{
 return (x * v.x + y * v.y + z * v.z + w * v.w);
};

void ModifyProjectionMatrix(const Vector4D& clipPlane)
{
 float matrix[16];
 Vector4D q;

 // Grab the current projection matrix from OpenGL
 glGetFloatv(GL_PROJECTION_MATRIX, matrix);

 // Transform the clip-space corner point opposite the
 // clipping plane into camera space by multiplying it
 // by the inverse of the projection matrix
 q.x = (sgn(clipPlane.x) + matrix[8]) / matrix[0];
 q.y = (sgn(clipPlane.y) + matrix[9]) / matrix[5];
 q.z = - 1.0F;
 q.w = (1.0F + matrix[10]) / matrix[14];

 // Calculate the scaled plane vector
 Vector4D c = clipPlane * (-2.0F / (clipPlane * q));

 // Replace the third row of the projection matrix
 matrix[2] = c.x;
 matrix[6] = c.y;
 matrix[10] = c.z + 1.0F;
 matrix[14] = c.w;

 // Load it back into OpenGL
 glMatrixMode(GL_PROJECTION);
 glLoadMatrix(matrix);
}
```

# Direct3D Implementation

In the Direct3D environment, camera space is lefthanded, and the near plane corresponds to the set of points for which the clip-space z-coordinate is 0. Thus, the value of the near clip plane listed in Table 2.6.1 should be changed to 〈0,0,1,0〉 for Direct3D applications. Consequently, the camera-space value of the near clip plane is simply given by M₃. This means that the entries of the third row of the projection