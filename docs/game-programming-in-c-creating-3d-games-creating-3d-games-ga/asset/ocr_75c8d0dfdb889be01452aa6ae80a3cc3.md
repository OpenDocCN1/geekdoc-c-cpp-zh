potentially have to return a collection of components rather than just a single pointer.

Also, the type information does not give inheritance information; you can't figure out `SkeletalMeshComponent` is a subclass of `MeshComponent`, as `GetType` for `SkeletalMeshComponent` just returns `TSkeletalMeshComponent`. To support inheritance information, you would need an approach that saves some hierarchy information as well.

With the basic type system in place, you can move on to more familiar steps. As with `Actor`, you need to create a virtual `LoadProperties` function in the base `Component` class and then override it for any subclasses, as needed. The implementations in the various subclasses are not necessarily straightforward. Listing 14.9 shows the implementation of `LoadProperties` for `MeshComponent`. Recall that `MeshComponent` has an `mMesh` member variable that's a pointer to the vertex data to draw. You don't want to specify the vertex directly in the JSON file; instead, you want to reference the gpmesh file. The code first checks for the `meshFile` property and then gets the corresponding mesh from the renderer.

# **Listing 14.9** `MeshComponent::LoadProperties` Implementation

Click here to view code image