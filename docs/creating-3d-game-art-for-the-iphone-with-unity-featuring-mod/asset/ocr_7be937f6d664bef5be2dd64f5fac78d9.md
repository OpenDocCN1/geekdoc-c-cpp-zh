![](bbox=[0.056, 0.109, 0.889, 0.6])

FIG 9.5 This image shows the Default Prefab from the Third-Person Controller for the iPhone available on UnityPrefabs.com.

# ## Setting up Colliders

In order to have your character react with the environment such as being able to move across the ground and stop when running into objects, you'll need to use Colliders.

Colliders can be very expensive on the iDevices and should be used with care. There are five types of Colliders you can use, and some are more expensive than others. In Fig. 9.6, you can see a diagram that shows each Collider type as they progress from cheap to expensive in terms of performance impact.

You can actually choose to have Unity iOS automatically create Colliders for you upon import by checking Generate Colliders in the Import Settings Dialog as shown in Fig. 9.7.

The Generate Colliders option will add a Mesh Collider to your object. The Mesh Collider builds a Collider based off the mesh it's applied to. It can