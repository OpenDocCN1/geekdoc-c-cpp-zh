You can notice that in our code snippet, we used the distance between the camera’s eye and its target instead of the distance between the camera’s eye and the object itself. The argument for doing this is that the camera’s target always represents the *direct* or *indirect* position of the followed object. An indirect case occurs when the target deviates from the actual position of the object after applying low-pass filtering and extrapolation.

# Implementing Human Behavior

We will now discuss the implementation of our human camera movement model in our camera model. The camera has a variety of data members and member functions. Here, we will introduce the most important ones.

At the beginning of the camera.h header file, where the Camera class is defined, there are some global constants. One of them defines the maximum length of arrays that are used in extrapolation of the camera’s target. It is called MAXEXTRAPOLLENGTH and its value, used by us, is 1000. This value should be greater than the maximum frame rate of the rendered scene in the used computer, because the lists defined with this length should store vectors of a second collected frame by frame.

Other important members of the Camera class are the Vector3f variables, which define the camera itself (eye, target, and up). The Vector3f arrays (objPosList, objPosDifList, objPosDifDifList, and upPosObjList) and float arrays (objFrameWeightList and sumWeight) are used in the extrapolation. The first three arrays are the collections of position, speed-like, and acceleration-like samples, while the fourth one is reserved for the low-pass filtered position samples. The first float array stores weights where we define the importance of the corresponding objPosDifList and objPosDifDifList elements, while the second list contains a precalculated sum of weights for each element number used in averaging.

These arrays store data chronologically. The elements indexed by 0 correspond to the actual frame, while another indexed by n represents the past, n frames ago.

Here you can see the spirit of the human behavior for our virtual camera model. This function (called placeObjectHereToFollow()) gets the actual position (objPos) of the followed object with a flag (lookAtItExactly) to know that the target should follow it directly or with human nature.

```
void placeObjectHereToFollow(Vector3f objPos,
                             bool lookAtItExactly = false) {
    if (actualFPS == 0.0) return;
}
```

The function starts with a control. If the actual frame rate is zero, which can happen for a while when the application first starts, we skip this execution to avoid malfunction.

Then we define those time-dependent parameters, which are calculated from the actual frame rate (actualFPS). The floating-point variables 1lengthForExtrpl and 1lengthForLPF and their integer versions (called iLengthForExtrpl and iLengthForLPF) contain the number of samples used in extrapolation or low-pass filtering. In other