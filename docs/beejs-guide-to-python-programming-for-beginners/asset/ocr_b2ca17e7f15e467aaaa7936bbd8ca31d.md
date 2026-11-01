So we need a ZipFile object that represents the ZIP file example.zip.

That is, we know the ZIP is named example.zip, and we need to go from that to a ZipFile object. Once we have the ZipFile object for example.zip, we can call printdir().

OK. So how do we do that? Time to get back to skimming docs! How do I create a ZipFile object?

Skim now!

We saw earlier this was the class:

```
zipfile.ZipFile
```

And a bit farther down, we have:

```
class zipfile.ZipFile(file, mode='r', compression=ZIP_STORED, allowZip64=True, compresslevel=None, *, strict_timestamps=True)
```

Open a ZIP file, where file can be a path to a file (a string), a file-like object or a path-like object.

Recognize that? It's a constructor!! That's what we want! We want to construct a ZipFile object from the string example.zip, and that's exactly what this does for us.

Continuing down, I'm not seeing anything else that helps us make a ZipFile object, so let's pursue this plan.

+   - Import the ZIP file functionality.
+   - Create a ZipFile object from example.zip.
+   - Print the table of contents with printdir() on that ZipFile object.

Let's go!

# Problem-solving step: **Carrying Out the Plan**

```
import zipfile
```

Check.

Okay—now we need to do something with that ZipFile constructor. Recall that since it's in the zipfile module, we have to refer to it as zipfile.ZipFile when we use it.

But, man, the docs are thick for the constructor. What is all that stuff?

Remember that any keyword argument with something after an equal sign is optional. We don't have to pass arguments for mode, compression, or any of those.

What we do have to pass in is the file, which is the filename to read. Let's do that, and we'll save the newly-constructed object in the variable zf:

```
# Important: make sure example.zip is in the same directory
# as this program!

zf = zipfile.ZipFile('example.zip')
```

Great!

And now that we have that object, let's print its directory:

```
zf.printdir()
```

And that gives us this output:

| File Name | Modified | Size |
|-----------|----------|------|
| hello.txt | 2020-02-09 15:12:20 | 6 |
| world.txt | 2020-02-09 15:12:24 | 7 |

Yes!

# Problem-solving step: **Looking Back.**