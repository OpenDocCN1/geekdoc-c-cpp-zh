if it doesn’t exist yet, its parent. If it’s a property-put, the resource has to exist, so we need to retrieve the resource itself. Then we do the appropriate update.

```
Download filesystem/filesystem_servlet.py

```python
def put(self):
    filesystem = GetFilesystem()
    root = filesystem.root
    url = self.request.path
    urlElements = url.split("/")
    resourcePath = None
    attr = None
    if urlElements[-1].startswith("~"):
        attr = urlElements[-1]
        resourcePath = urlElements[:-1]
    else:
        resourcePath = urlElements
    resource = filesystem.getResourceFromChildByList(root, resourcePath)
    if resource is None:
        parent = filesystem.getResourceFromChildByList(root,
                                                       resourcePath[0:-1])
        name = resourcePath[-1]
        if parent is None:
            self.response.set_status(404,
                                     "Parent dir of new resource not found")
        else:
            resource = Resource(content = self.request.body, attributes=[],
                                children=[])
            resource.put()
            dirEntry = DirectoryEntry(name=name, resource=resource)
            parent.children.append(dirEntry)
            parent.put()
            self.response.set_status(100, "Resource created")
            return
    else:
        resource.content=self.request.body
        resource.put()
        self.response.set_status(100, "Resource updated")
```
```

Everything is just like GET up to the point where we try to retrieve the resource. In GET, if we couldn’t find the requested resource, we returned an error. In PUT, we just try to create the resource. In order to create it, we need to try to get the parent resource. If we can’t find that, we return an error. But if we can find the parent, we go ahead and create the new resource as its child.

We can create a new resource by instantiating the model class. Each of the properties of the model is a named parameter to the constructor. Once it’s created, we save it to datastore using put().