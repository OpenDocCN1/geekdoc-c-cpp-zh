transform for every bone in bind pose. To encapsulate the skeleton data, you can declare a Skeleton class, as shown in Listing 12.4.

# Listing 12.4 Skeleton Declaration

Click here to view code image

```
class Skeleton
{
public:
    // Definition for each bone in the skeleton
    struct Bone
    {
        BoneTransform mLocalBindPose;
        std::string mName;
        int mParent;
    };

    // Load from a file
    bool Load(const std::string& fileName);

    // Getter functions
    size_t GetNumBones() const { return mBones.size(); }
```