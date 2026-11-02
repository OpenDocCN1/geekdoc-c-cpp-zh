
NetworkInformation.getConnectionProfiles (which we saw in Chapter 4). Similarly, StorageFolder.getFilesAsync provides a vector view of StorageFile objects. The user's preferred languages in the Windows.System.UserProfile.GlobalizationPreferences object is a vector view of strings. And you can always get a read-only view for any given read-write vector through the latter's getView method.

Now because a vector is just a more capable iterator, guess what? You can just treat a vector like an array. For example, the Folder enumeration sample uses StorageFolder.getFilesAsync and getItemsAsync to list the contents of your various media libraries, using forEach to iterate the array that those APIs produce. Using that example, here's what I meant earlier when I mentioned that Visual Studio shows only the IVector members—the items from getItemsAsync doesn't show array methods, but we can clearly call forEach (circled):

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_308_0.png)

What all this means for data binding, to return to the context of this chapter, is that it's no problem to create a WinJS.Binding.List from the WinRT methods and properties that produce vectors and vector views, because those collections are projected as arrays.

**Tip** If you're enumerating folder contents to create a gallery experience—that is, displaying thumbnails of files in a control like the WinJS.UI.ListView—always use Windows.Storage.StorageFile.getThumbnailAsync or StorageFile.getScaledImageAsThumbnailAsync to retrieve a small image for your data source, which can be passed to URL.createObjectURL and the result assigned to an img element. This performs far better in both speed and memory efficiency, as the API draws from the thumbnails cache instead of loading the entire file contents (as happens if you call URL.createObjectURL on the full StorageFile). See the File and folder thumbnail sample for demonstrations.

## Maps and Property Sets

A map (IMap<K, V>) and its read-only map view companion (IMapView<K, V>) are additional derivations of the basic iterator. A map is composed of key-value pairs, where the keys and values can both be arbitrary types.61 A closely related construct is the property set (IPropertySet), which relates to the map. The difference is that maps and map views are used (like vectors) to return collections from WinRT APIs and to handle certain properties of WinRT objects. Property sets, for their part, as used (like basic iterators) as input arguments to WinRT APIs.

It’s important to note right up front that maps and property sets are not projected as arrays. They do support value lookup through the [ ] operator, but otherwise do not have array methods. A map, instead, has methods (from IMap) called lookup (same as [ ]), insert, remove, clear, and hasKey, along with a size property and a getView method like the vector. A map view shares hasKey, lookup, and size, and adds a split method. You can also pass a map or map view to Object.keys to retrieve an array of keys.

A property set has a more extensive interface, but let me come back to that in a bit.

The generic term for maps and property sets alike is a dictionary. A dictionary does just what the word means in colloquial language: it lets you look up an item (similar to a definition) in a collection (the dictionary) by a key (such as a word). This is very useful when the collection you’re working with doesn’t store items in a linear or indexed array, or doesn’t have a need to do so. For example, when working with the Windows.Storage.Pickers.FileSavePicker class, you give the user a choice of file types through its fileTypeChoices property. This property is interesting because its type is IMap<String, IVector>, meaning that it’s a map between a string key and a value that is itself an array. This makes sense, because you want to use something like “JPEG” for a key while yet mapping that single key to a group of values like “.jpg” and “.jpeg”.

Maps are also used extensively when working with file properties, where you have access to a deeper hierarchy of metadata that’s composed of key-value pairs. This is the same metadata that you can explore if you right-click a file in Windows Explorer and click the details tab, as shown here for a picture I took on a trip to Egypt where the camera recorded exposure details and so forth:

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_310_0.png)

As we'll see in Chapter 11, "The Story of State, Part 2," the `Windows.Storage.FileProperties` API is how you get to all this metadata. Images provide an `ImageProperties` object, whose `retrievePropertiesAsync` produces a map containing the metadata. You can play with this in the `Simple Imaging` sample if you'd like, where once you've obtained a map you can access individual properties by name (`retrievedProps` is the map):

```
retrievedProps["System.Photo.ExposureTime"]
```

On the flip side of this metadata scene is where we encounter property sets. Again, these are a form of dictionary like maps but one that an app needs to create for input to methods like `ImageProperties.savePropertiesAsync`. This is why `Windows.Foundation.Collections` has a concrete `PropertySet` class and not just an interface, because then we can `new` up an instance like so:

```
var properties = new Windows.Foundation.Collections.PropertySet();
```

and create key-value pairs with the `[ ]` operator:

```
properties["System.GPS.LatitudeNumerator"] = latNum;
```

or with the `insert` method:

```
properties.insert("System.GPS.LatitudeNumerator", latNum);
```

Be mindful that while the documentation for PropertySet lists quite a few methods and properties, only some of them are projected into JavaScript:
- Properties: size
- Lookup methods: [ ], lookup, hasKey, first (returns an iterator for the key-value pairs)
- Manipulation methods: clear, insert, remove
- Other: getView (retrieves a map view) and the mapChanged event

In summary, maps and property sets are distinct collection constructs that must be worked with through their own methods and properties. Vectors, on the other hand, are projected into JavaScript as an array and are thus suitable for data binding. If you want to bind to a map or property set, on the other hand, you'll need to maintain an array copy.

## WinJS Binding Lists

The WinJS.Binding.List object is the core of collection-based data binding in WinJS and is what you use with both templates and collection controls, as will be discussed in this chapter and the next. That is, the name of the ListView control is quite apt: it's a view of a list but not the list itself. That list is a WinJS.Binding.List, which I'll just refer to as List or "list" for convenience.

A List takes a JavaScript array and makes it observable, because such a process means more than WinJS.Binding.as does with a single object. The array in question can contain any kind of objects, from simple values to complex objects and other arrays. All it takes is a new.

```
list = new WinJS.Binding.List(dataArray);
```

Note that you can typically build a List with a sparse array meaning that you can have noncontiguous indices within the array (see Using Arrays).

Once created, the List provides a number of array-like methods and properties, namely length, concat, every, filter, forEach, indexOf, join (using a comma), lastIndexOf, map, push, pop, reduce, reduceRight, reverse, shift, slice, sort, and unshift. These operate exactly like they do with a typical array except that functions like concat produce another List rather than an array. The List also provides additional lookup and management methods: getAt, getItem, getItemFromKey, indexOfKey, move, setAt, and some. I'll leave you to check out the details of all these as needed, as they are all very simple and straightforward.

**Hint** You can create an empty List without an array, using new WinJS.Binding.List(). You then use methods like push to populate the list.

What's much more interesting are those List features that apply more to data binding in particular, which come under four groups:
