not using Core Data, we would be describing every entity, attribute, and relationship inside of the sync schema. Fortunately, since we are using Core Data, that part is not necessary. What this leaves to be included in the schema is to define the data classes, the localization, and the icon to be used by Sync Services whenever it is talking about our data class. When we are done, we will have another bundle to be included in our application that we will reference when dealing with Sync Services.

# ## Setting Up the Sync Schema Subproject

Just like the Spotlight and Quick Look subprojects that we created in Chapter 7, *Spotlight, Quick Look, and Core Data*, on page 114, we will add a third subproject to our recipes application. Just like the previous two, the sync schema project template is under the Standard Apple Plugins section in Xcode. Once the subproject is created, we drag the project into our main project and define it as a dependency in the application target. Once the dependency is set up, then add the .syncschema bundle to the Copy Bundle Resources phase of the target.

# ## Creating the Schema.plist

Although it is possible to add custom code to a sync schema to help display the data when the sync error dialog box is displayed, for our purposes we really need to set up only the Schema.plist file. The header and implementation files that are created with the template can be removed because we will not be needing them.

The Schema.plist file describes everything that Sync Services needs to know about our data. For our needs, we need to set three keys within this plist: DataClasses, ManagedObjectModels, and Name.

# ### DataClasses Key

The DataClasses key has two values, a Name and an ImagePath. The Name value is meant to be localized and therefore does not need to be user friendly in this file. For our recipes, I named the data class com.pragprog.GrokkingRecipes. The only requirement is that this name be unique. Therefore, a reverse dot notation will help to guarantee that. The other value, ImagePath, needs to point to an image file that Sync Services will use whenever it is referring to our data. For example, this image is used in the system preferences and in the data change alert dialog boxes. For our needs, the application icon is sufficient for this, so we include a copy of it within the sync schema bundle.