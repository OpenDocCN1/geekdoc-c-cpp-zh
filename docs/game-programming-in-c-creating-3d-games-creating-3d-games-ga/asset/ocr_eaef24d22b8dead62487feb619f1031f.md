To define the overall skeleton, for each bone you need to know the name of the bone, the parent of the bone, and its bone transform. For the bone transform, you specifically store the local pose (the transform from the parent) when the overall skeleton is in the bind pose.

One way to store these bones is in an array. Index 0 of the array corresponds to the root bone, and then each subsequent bone references its parent by an index number. For the example in Figure 12.2, the spine bone, stored in index 1, has a parent index of 0 because the root bone is its parent. Similarly, the hip bone, stored in index 2, has a parent of index 1.

| Index | 0 | 1 | 2 | 3 | 4 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Bone | Name: Root Parent: -1 Local Pose: ... | Name: Spine Parent: 0 Local Pose: ... | Name: HipL Parent: 1 Local Pose: ... | Name: HipR Parent: 1 Local Pose: ... | ... |

Figure 12.2 Representation of skeleton as an array of bones

This leads to the following `Bone` struct that contains the local bind pose transform, a bone name, and a parent index:

Click here to view code image

```
struct Bone
{
    BoneTransform mLocalBindPose;
    std::string mName;
}
```