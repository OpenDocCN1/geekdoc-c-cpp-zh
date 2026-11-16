```
BoneTransform BoneTransform::Interpolate(const BoneTr
const BoneTransform& b, float f)
{
BoneTransform retVal;
retVal.mRotation = Quaternion::Slerp(a.mRotation,
retVal.mTranslation = Vector3::Lerp(a.mTranslation
b.mTranslation, f);
return retVal;
}
```

Then, if the game must show a state between two different frames, you can interpolate the transforms of each bone to get the current local pose.

# Skinning

Skinning involves associating vertices in the 3D model with one or more bones in the corresponding skeleton. (This is different from the term skinning in a non-animation context.) Then, when drawing a vertex, the position and orientation of any associated bones influence the position of the vertex. Because the skinning of a model does not change during the game, the skinning information is an attribute of each vertex.