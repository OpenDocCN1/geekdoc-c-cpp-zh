```
return true;
}

return false;
}
```

First, you open the file for reading in binary mode. Next,
you read in the header via the `read` function. Much as
with `write`, `read` takes in a `char*` for where to write
and the number of bytes to read from the file. Next, you
verify that the signature and version in the header match
what is expected; if they don't, you can't load the file.

After this, you read in all the texture filenames and load
them, though we omit that code from Listing 14.16 to
save space. Next, you allocate memory to store the vertex
and index buffers, and you use `read` to grab the data
from the file. Once you have the vertex and index data,
you can construct the `VertexArray` object and pass in
all the information it needs. You need to make sure to
clean up the memory and set the `mBox` and `mRadius`
members before returning.

Note that `LoadBinary` returns `false` if the file fails to
load. This way, the `Mesh::Load` code first tries to load
the binary file. If it succeeds, that's it. Otherwise, it can
proceed using the JSON parsing code from before: