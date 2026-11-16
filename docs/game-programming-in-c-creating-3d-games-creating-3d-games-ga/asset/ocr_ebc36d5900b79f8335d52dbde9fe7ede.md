sound occlusion, as illustrated in Figure 7-5(a).

![](bbox=[0.16, 0.14, 0.73, 0.3])

Figure 7.5 Sound occlusion (a) and testing for occlusion (b)

Sound occlusion occurs when a sound does not have a direct path from emitter to listener. Instead, the sound must travel through some material to reach the listener. The predominant result of sound occlusion is a low-pass filter, which means a reduction in volume of higher-frequency sounds.

Implementing occlusion involves two separate tasks: detection of occlusion and modification of occluded sounds. One approach for detection is to draw line segments between the emitter and an arc around the listener, as in Figure 7-5(b). If all line segments can reach the listener without hitting any objects, there is no occlusion. If only some line segments reach, there's partial occlusion, and if none reach, there's full occlusion. This style of detection requires the collision calculations covered in Chapter 10, “Collision Detection.”

Modifying occluded sounds in FMOD is simple. However, it requires calls into the Low Level API. First,