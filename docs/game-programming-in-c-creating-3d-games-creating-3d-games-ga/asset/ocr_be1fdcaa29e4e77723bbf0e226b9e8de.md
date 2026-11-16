```
const class Skeleton* inSkeleton, float inTime)

private:

// Number of bones for the animation

size_t mNumBones;

// Number of frames in the animation

size_t mNumFrames;

// Duration of the animation in seconds

float mDuration;

// Duration of each frame in animation

float mFrameDuration;

// Transform information for each frame on the tra
// Each index in the outer vector is a bone, inner
std::vector<std::vector<BoneTransform>> mTracks;

};
```

The job of the GetGlobalPoseAtTime function is to compute the global pose matrices for each bone in the skeleton at the specified inTime. It writes these global pose matrices to the provided outPoses std::vector of matrices. For now, you can ignore the inTime parameter and just hard-code the function so that it uses frame 0. This way, you can first get the game to draw the first frame of the animation properly. The