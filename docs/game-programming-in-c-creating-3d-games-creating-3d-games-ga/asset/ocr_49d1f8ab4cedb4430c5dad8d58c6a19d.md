```
```cpp
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
    const Bone& GetBone(size_t idx) const { return mBones[idx]; }
    const std::vector<Bone>& GetBones() const { return mBones; }
    const std::vector<Matrix4>& GetGlobalInvBindPoses() const
    {
        return mGlobalInvBindPoses;
    }

protected:
    // Computes the global inverse bind pose for each bone
    // (Called when loading the skeleton)
    void ComputeGlobalInvBindPose();

private:
    // The bones in the skeleton
    std::vector<Bone> mBones;
    // The global inverse bind poses for each bone
    std::vector<Matrix4> mGlobalInvBindPoses;
};
```
```