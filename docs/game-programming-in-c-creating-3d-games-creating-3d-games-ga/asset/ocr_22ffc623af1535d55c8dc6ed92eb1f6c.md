```
// Wrap around anim time if past duration
while (mAnimTime > mAnimation->GetDuration())
{ mAnimTime -= mAnimation->GetDuration(); }

// Recompute matrix palette
ComputeMatrixPalette();
}
}
```

Here, all you do is update mAnimTime based on delta time and the animation play rate. You also wrap mAnimTime around as the animation loops. This works correctly even when transitioning from the last frame of the animation to the first because, as mentioned earlier, the animation data duplicates the first frame at the end of the track.

Finally, Update calls ComputeMatrixPalette. This function uses GetGlobalPoseAtTime to calculate the new matrix palette for this frame.

Because SkeletalMeshComponent is a component, the owning actor calls Update every frame. Then in the “generate outputs” phase of the game loop, the SkeletalMeshComponent draws with this new matrix palette as usual, which means the animation now