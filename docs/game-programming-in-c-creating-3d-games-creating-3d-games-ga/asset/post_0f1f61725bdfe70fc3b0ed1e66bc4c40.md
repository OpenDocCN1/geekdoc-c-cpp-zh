
```
{
    "version":1,
    "bonecount":68,
    "bones":[
        {
            "name":"root",
            "parent":-1,
            "bindpose":{
                "rot":[0.000000,0.000000,0.000000,1.000000],
                "trans":[0.000000,0.000000,0.000000]
            },
        },
        {
            "name":"pelvis",
            "parent":0,
            "bindpose":{
                "rot":[0.001285,0.707106,-0.001285,-0.707106],
                "trans":[0.000000,-1.056153,96.750603]
            },
        },
    ],
    // ...
}
```

```
class SkeletalMeshComponent : public MechComponent
{
public:
    SkeletalMeshComponent(class Actor* owner);
    // Draw this mesh component
    void Draw(class Shader* shader) override;
};
```

```
// Draw any skinned meshes now
mSkinnedShader->SetActive();
// Update view-projection matrix
mSkinnedShader->SetMatrixUniform("uViewProj", mView * mProjection);
// Update lighting uniforms
SetLightUniforms(mSkinnedShader);
for (auto sk : mSkeletalMeshes)
{
    if (sk->GetVisible())
    {
        sk->Draw(mSkinnedShader);
    }
}
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
void Skeleton::ComputeGlobalInvBindPose()
{
    // Resize to number of bones, which automatically fills identity
    mGlobalInvBindPoses.resize(GetNumBones());

    // Step 1: Compute global bind pose for each bone
    // The global bind pose for root is just the local bind pose
    mGlobalInvBindPoses[0] = mBones[0].mLocalBindPose.ToMatrix();

    // Each remaining bone's global bind pose is its local pose
    // multiplied by the parent's global bind pose
    for (size_t i = 1; i < mGlobalInvBindPoses.size(); ++i)
    {
        Matrix4 localMat = mBones[i].mLocalBindPose.ToMatrix();
        mGlobalInvBindPoses[i] = localMat *
            mGlobalInvBindPoses[mBones[i].mParent];
    }

    // Step 2: Invert each matrix
    for (size_t i = 0; i < mGlobalInvBindPoses.size(); ++i)
    {
        mGlobalInvBindPoses[i].Invert();
    }
}
```

```
{
  "version":1,
  "sequence":{
    "frames":19,
    "duration":0.60000,
    "bonecount":68,
    "tracks":{
      "bone":0,
      "transforms":[
        {
          "rot":[-0.500199,0.499801,-0.499801,0.500199],
          "trans":[0.000000,0.000000,0.000000]
        },
        {
          "rot":[-0.500199,0.499801,-0.499801,0.500199],
          "trans":[0.000000,0.000000,0.000000]
        },
        // Additional transforms up to frame count
      ],
      // Additional tracks for each bone
      // ...
    }
  }
}
}
```

```
class Animation
{
public:
    bool Load(const std::string& fileName);

    size_t GetNumBones() const { return mNumBones; }
    size_t GetNumFrames() const { return mNumFrames; }
    float GetDuration() const { return mDuration; }
    float GetFrameDuration() const { return mFrameDuration; }

    // Fills the provided vector with the global (current) pose matrices
    // for each bone at the specified time in the animation.
    void GetGlobalPoseAtTime(std::vector<Matrix4x4>& outPoses,
        const class Skeleton* inSkeleton, float inTime) const;

private:
    // Number of bones for the animation
    size_t mNumBones;

    // Number of frames in the animation
    size_t mNumFrames;

    // Duration of the animation in seconds
    float mDuration;

    // Duration of each frame in animation
    float mFrameDuration;

    // Transform information for each frame on the track
    // Each index in the outer vector is a bone, inner vector is a frame
    std::vector<std::vector<BoneTransform>> mTracks;
};
```

```
void Animation::GetGlobalPoseAtTime(std::vector<Matrix4x4>& outPoses,
const Skeleton& inSkeleton, float inTime) const
{
  // Resize the outPoses vector if needed
  if (outPoses.size() != mNumBones)
  {
    outPoses.resize(mNumBones);
  }

  // For now, just compute the pose for every bone at frame 0
  const int frame = 0;

  // Set the pose for the root
  // Does the root have a track?
  if (mTracks[0].size() > 0)
  {
    // The global pose for the root is just its local pose
    outPoses[0] = mTracks[0][frame].ToMatrix();
  }
  else
  {
    outPoses[0] = Matrix4::Identity;
  }

  const std::vector<Skeleton::Bone>& bones = inSkeleton->GetBones();
  // Now compute the global pose matrices for every other bone
  for (size_t bone = 1; bone < mNumBones; bone++)
  {
      Matrix4 localMat; // Defaults to identity
      if (mTracks[bone].size() > 0)
      {
          localMat = mTracks[bone][frame].ToMatrix();
      }
      outPoses[bone] = localMat * outPoses[bones[bone].mParent];
  }
}
```

```
const size_t MAX_SKELETON_BONES = 96;
struct MatrixPalette
{
    Matrix4 mEntry[MAX_SKELETON_BONES];
};
```

```cpp
// Matrix palette
MatrixPalette mPalette;
// Animation currently playing
class Animation* mAnimation;
// Play rate of animation (1.0 is normal speed)
float mAnimPlayRate;
// Current time in the animation
float mAnimTime;
```

```
void SkeletalMeshComponent::ComputeMatrixPalette()
{
    const std::vector<Matrix4x4>& globalInvBindPoses =
        mSkeleton->GetGlobalInvBindPoses();

    std::vector<Matrix4x4> currentPoses;
    mAnimation->GetGlobalPoseAtTime(currentPoses, mSkeleton,
                                    mAnimTime);

    // Setup the palette for each bone
    for (size_t i = 0; i < mSkeleton->GetNumBones(); i++)
    {
        // Global inverse bind pose matrix times current pose matrix
        mPalette.mEntry[i] = globalInvBindPoses[i] * currentPoses[i];
    }
}
```

```cpp
float SkeletalMeshComponent::PlayAnimation(const Animation* anim,
    float playRate)
{
    mAnimation = anim;
    mAnimTime = 0.0f;
    mAnimPlayRate = playRate;

    if (!mAnimation) { return 0.0f; }
    ComputeMatrixPalette();

    return mAnimation->GetDuration();
}
```

```
void main()
{
    // Convert position to homogeneous coordinates
    vec4 pos = vec4(inPosition, 1.0);

    // Skin the position
    vec4 skinnedPos = (pos * uMatrixPalette[inSkinBones.x]) *
    inSkinWeights.x;
    skinnedPos += (pos * uMatrixPalette[inSkinBones.y]) * inSkinWeights.y;
    skinnedPos += (pos * uMatrixPalette[inSkinBones.z]) * inSkinWeights.z;
    skinnedPos += (pos * uMatrixPalette[inSkinBones.w]) * inSkinWeights.w;
    // Transform position to world space
    skinnedPos = skinnedPos * uWorldTransform;

    // Save world position
    fragWorldPos = skinnedPos.xyz;

    // Transform to clip space
    gl_Position = skinnedPos * uViewProj;

    // Skin the vertex normal
    vec4 skinnedNormal = vec4(inNormal, 0.0f);
    skinnedNormal =
    (skinnedNormal * uMatrixPalette[inSkinBones.x]) * inSkinWeights.x
    + (skinnedNormal * uMatrixPalette[inSkinBones.y]) * inSkinWeights.y
    + (skinnedNormal * uMatrixPalette[inSkinBones.z]) * inSkinWeights.z
    + (skinnedNormal * uMatrixPalette[inSkinBones.w]) * inSkinWeights.w;
    // Transform normal into world space (w = 0)
    fragNormal = (skinnedNormal * uWorldTransform).xyz;

    // Pass along the texture coordinate to frag shader
    fragTexCoord = inTexCoord;
}
```
