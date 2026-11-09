
```python
class Filesystem(db.Model):
    root = db.Reference(Resource)

    def GetRoot(self):
        return self.root

    def GetResource(self, path):
        path_elements = path.split("/")
        return self.GetResourceFromChildByList(self.root, path_elements)

    def GetResourceFromChildByList(self, resource, path_elements):
        if path_elements == []:
            return resource
        else:
            for direntry in resource.children:
                if direntry.name == path_elements[0]:
                    return self.GetResourceFromChildByList(direntry.resource,
                                                           path_elements[1:])
        return None
```

## Implementing File Retrieval Using GET

We've worked out a basic filesystem model; the next thing to do is implement it. The datastore parts of this are pretty easy—at least at first. To do a basic filesystem, it’s pretty much just a series of full-object GETs and PUTs. There’s a bit of work to get the URLs mapped, but it’s nothing particularly different from what we’ve seen before. But as you’ll see, once we have the basics, we can move on to some more interesting things, like searching the filesystem based on property values.

Let’s start with the basics. What do we want users to be able to do with our filesystem?

- 1. Create a resource. This involves creating the resource object, setting its properties, storing its content, and modifying its parent resource to provide a directory entry to the new resource.
- 2. Retrieve a resource’s contents.
- 3. Set and retrieve resource properties.
- 4. Update a resource’s content.

We must map these actions onto the basic HTTP operations: GET, PUT, and POST. Retrieving a resource’s content or its properties is clearly a GET operation. Creating a new resource or updating its content is PUT.

In fact, for now, we really don’t need POST at all: we’ll use GET for all retrieves, and we’ll use PUT for all stores.

Now we need to think about how to structure our URLs. If we ignore attributes, it’s easy—we have simple paths in a URL, and the standard URL syntax was designed exactly for that. For attributes, it’s a bit trickier. We could use CGI parameters to modify the HTTP call, or we could create a way of encoding attributes into the URL. The classic REST style calls for the latter approach. An attribute is a kind of data accessible by the service; each piece of uniquely identifiable data should have its own URL.

Attributes are bits of metadata for a resource, so their URLs should be based on the URL of the file they’re associated with. In order to prevent confusion between an attribute of a file and a member of a directory, we’ll prefix attributes with “~”, which we won’t allow as a path character in the name of a resource. Given a resource with URL R, its attribute a1 will be accessed by a URL R/~a1.

We can make a first version of our filesystem service with a GET handler:

```python
# Download filesystem/filesystem_servlet.py
class FilesystemResourceHandler(webapp.RequestHandler):
    def GetFilesystem(self):
        query = Filesystem.gql("")
        return query

    def get(self):
        filesystem = self.GetFilesystem()
        root = filesystem.root
        url = self.request.path
        urlElements = url.split("/")
        # And then check if it's a content request or an attribute request.
        # if the first char of the last name element is "~", then it's
        # an attribute.
        resourcePath = None
        attr = None
        if urlElements[-1].startswith("~"):
            attr = urlElements[-1][1:]
            resourcePath = urlElements[:-1]
        else:
            resourcePath = urlElements
        resource = filesystem.GetResourceFromChildByList(root, resourcePath)
        if resource is None:
            self.response.set_status(404)
            return
        if attr is not None:
            result = resource.getAttribute(attr)
            if result is None:
                self.response.set_status(404)
                return
            else:
                self.response.out.write(str(result))
        else:
            self.response.out.write(resource.content.data)
```

- 1. First, typically for a cloud application, we need to call a retrieval function to fetch the filesystem root object. We know how to write that: it’s just a simple datastore retrieval.
- 2. With the filesystem, we can get the root resource—that is, the root directory of our filesystem.
- 3. Then we go to the request, and from it we retrieve the path for the resource that we want to retrieve.
- 4. We parse the path to see if it’s a request for an attribute or for the resource content.
- 5. We retrieve the resource object using the method we wrote earlier in the chapter.
- 6. If the attempt to retrieve the resource fails, it returns null. So we generate a 404 response (the HTTP response for “resource not found”).
- 7. If the URL included an attribute name, we retrieve the attribute and return it in the content of the result message. If we don’t specify the result code, it will default to the success code, and the content-type will default to UTF-8 text. Since those are both what we want, all we need to do is write the attribute value to the response stream.
- 8. Otherwise, we use the datastore reference auto-retrieve to get the resource content and write it to the stream. Again, the defaults will work perfectly: when we write a blob to the response output stream, if the blob is just text characters, it will default to UTF-8; if it’s got any nontext bytes, it will default to a byte stream.

## Implementing File Storage Using PUT

The interesting thing about implementing file storage is that when you PUT the files, you might need to also update the parent of the file in order to create a directory entry for the new resource.

The code is pretty similar to GET. We start off by parsing the path. If the PUT is a content-put, we need to retrieve either the resource or, if it doesn’t exist yet, its parent. If it’s a property-put, the resource has to exist, so we need to retrieve the resource itself. Then we do the appropriate update.

```python
# Download filesystem/filesystem_servlet.py
def put(self):
    filesystem = self.GetFilesystem()
    root = filesystem.root
    url = self.request.path
    urlElements = url.split("/")
    resourcePath = None
    attr = None
    if urlElements[-1].startswith("~"):
        attr = urlElements[-1][1:]
        resourcePath = urlElements[:-1]
    else:
        resourcePath = urlElements
    resource = filesystem.GetResourceFromChildByList(root, resourcePath)
    if resource is None:
        parent = filesystem.GetResourceFromChildByList(root,
                                                       resourcePath[0:-1])
        name = resourcePath[-1]
        if parent is None:
            self.response.set_status(404,
                                     "Parent dir of new resource not found")
        else:
            resource = Resource(content=self.request.body, attributes=[],
                                children=[])
            resource.put()
            dirEntry = DirectoryEntry(name=name, resource=resource)
            parent.children.append(dirEntry)
            parent.put()
            self.response.set_status(100, "Resource created")
            return
    else:
        resource.content = self.request.body
        resource.put()
        self.response.set_status(100, "Resource updated")
```

Everything is just like GET up to the point where we try to retrieve the resource. In GET, if we couldn’t find the requested resource, we returned an error. In PUT, we just try to create the resource. In order to create it, we need to try to get the parent resource. If we can’t find that, we return an error. But if we can find the parent, we go ahead and create the new resource as its child.

We can create a new resource by instantiating the model class. Each of the properties of the model is a named parameter to the constructor. Once it’s created, we save it to datastore using put().
