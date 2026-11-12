![](bbox=[0.03, 0.107, 0.891, 0.57])

FIG 4.7 Using Sections, the Vertex Count Is Dramatically Reduced.

move down the hall and turn left in order to see more of the level. The goal is to visualize your level and decide what areas will be visible to the camera's view frustum at a given time. The Occlusion Culling tools in Unity iOS will provide a similar optimization, but it's an Advanced License feature. Also, in order to properly use Occlusion Culling, you'll need to have your geometry broken into sensibly sized pieces as we've discussed in this chapter. So by following these principles of dividing up the level, you'll also be creating the correct geometry for using Occlusion Culling if you upgrade to or already have the Advanced License.

When building any objects for Unity IOS and the iDevices, I adopt the mantra, "Build to Batch." When creating your own content, you should always stick to this important concept in order to keep your mind focused on building optimized content.

> > *The goal is to visualize your level and decide what areas will be visible to the camera's view frustum at a given time.*