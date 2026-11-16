# 10.5 Future Work

We've presented in this article a means in which to offload the overhead of creating command buffers to separate threads in a device API agnostic manner and use a camera-centric design to ensure proper load balancing across multiple threads. As we continue to take greater advantage of our rendering APIs for general purpose computing, the ability to properly break up work based upon packets of rendering data will continue to be important.

There are many project- and system-specific issues that are related to this process that are beyond the scope of this article. For completeness however, we briefly describe them here and leave the nitty-gritty details as an exercise for the reader.

# Sorting and Instancing

RenderCommand objects provide excellent dynamic primitives for instancing evaluation. Once all the objects for a render view have been culled and added to a RenderCommand buffer, it is trivial at that point to define multiple types of sorting operations that can organize the RenderCommand objects in the buffer in various ways. Sorting by material index, vertex data, and object type often lends itself to a sorting process that combines objects in the command buffer in such a manner that multiple draw commands can be removed and a single command that uses instancing can be used. And if you're generating your RenderCommand structures dynamically, you can easily remove the original commands and insert the new instanced version. On some hardware, this may be a more performance friendly method of sorting by data, as your RenderCommand can take better usage of processor caches and reduce memory traversal that would normally be required when walking your object list.

# Better Load Balancing