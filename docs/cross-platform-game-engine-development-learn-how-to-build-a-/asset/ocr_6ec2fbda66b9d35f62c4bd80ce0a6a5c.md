to de- and serialize other components.
As you can see, we are including all component types here because we are going
to de- and serialize all of them. The constructor of the serializer takes a pointer to
the registry where all entities and components are stored. The deserialize function
takes the root node of entities, and the serialize function takes a reference to the
buffer where everything will be stored before being exported to a YAML file.
Let's take a look at each function's implementation specifically.

```
engine/src/ecs/serializer.h
FUSE_INLINE void deserialize(YAML::Node nodes) {
  // clear registry
  _registry->clear();

  // deserialize entities
  for (auto node : nodes) {
    ecs::entity e(_registry);
    deserialize_info(node, e);
    deserialize_transform(node, e);
    deserialize_rigidbody(node, e);
    deserialize_collider(node, e);
    deserialize_sprite(node, e);
    deserialize_animation(node, e);
    deserialize_text(node, e);
    deserialize_script(node, e);
  }
}
```

This function starts by making sure that the registry is cleared. This will prevent
the data loaded to be added on top of the already existing data in the registry.
Then we will loop through the entity's node given as an argument. For each node,
we will create an entity and call for each component type the deserialize function.
Don't worry about all the functions called here we will implement each one of
them in just a moment.

The next code snippet shows the definition of the serialize function. This function
takes a reference to an emitter as an argument. It starts by creating a sequence
called "entities", which is where all our entities will be listed.
Then we follow up by adding a map for each in which the entity's components
will be listed. Similar to the deserialize function, we are calling the serialize
function for each component type, passing the entity we want to retrieve the
component from.

Note : it is required to close all the nodes we have opened. Because all entities