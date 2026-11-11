```
```text
[data retain];
[image release];
    image = data;
}
```
```

In the accessor methods that we added to the PPRecipe object, we are retrieving the image data that is stored on the disk at imagePath. When the data is being set and the imagePath is not set, then we will create a new file in our Application Support directory and save it. These accessors now allow for the image to be passed around for Sync Services without it being stored in the repository.

As for the rest of the attributes and relationships, they are all flagged to be synced, and only the name attribute is flagged to be an identity property.

# RecipeIngredient Settings

The RecipeIngredient entity is an unusual one to sync. Since it is basically a join table (to borrow from database terminology), there is no attribute that identifies it as unique. Therefore, we will sync its one attribute, quantify, but we will flag its relationships as the identity properties. By flagging all three relationships as the identity of the record, we are guaranteed uniqueness for each combination of Ingredient, Recipe, and UnitOfMeasure.

# Type Settings

For the Type entity, we are syncing this object only to preserve the relationships across sync clients. Although this data will never change and therefore does not really need to be synced, we do want to sync the relationships between Type entities and Recipe entities. Therefore, we flag the name as the identity property and include its relationships in the sync.

# UnitOfMeasure

Like the Author entity, this entity has the name attribute as its identity property and has its relationships included in the sync.

# 8.3  Creating the Sync Schema

Now that our data model is ready for syncing, it is time to build the sync schema itself. The sync schema is used by Mac OS X to describe our interaction with and integration into the syncing ecosystem. If we were