```
```python
if result is None:
    self.response.error(404)
    self.response.out.write(str(result))
    return
else:
    self.response.out.write(resource.content.data)
```
```

+   1. First, typically for a cloud application, we need to call a retrieval function to fetch the filesystem root object. We know how to write that: it’s just a simple datastore retrieval.
+   2. With the filesystem, we can get the root resource—that is, the root directory of our filesystem.
+   3. Then we go to the request, and from it we retrieve the path for the resource that we want to retrieve.
+   4. We parse the path to see if it’s a request for an attribute or for the resource content.
+   5. We retrieve the resource object using the method we wrote earlier in the chapter.
+   6. If the attempt to retrieve the resource fails, it returns null. So we generate a 404 response (the HTTP response for “resource not found”).
+   7. If the URL included an attribute name, we retrieve the attribute and return it in the content of the result message. If we don’t specify the result code, it will default to the success code, and the content-type will default to UTF-8 text. Since those are both what we want, all we need to do is write the attribute value to the response stream.
+   8. Otherwise, we use the datastore reference auto-retrieve to get the resource content and write it to the stream. Again, the defaults will work perfectly: when we write a blob to the response output stream, if the blob is just text characters, it will default to UTF-8; if it’s got any nontext bytes, it will default to a byte stream.

# Implementing File Storage Using PUT

The interesting thing about implementing file storage is that when you PUT the files, you might need to also update the parent of the file in order to create a directory entry for the new resource.

The code is pretty similar to GET. We start off by parsing the path. If the PUT is a content-put, we need to retrieve either the resource or,