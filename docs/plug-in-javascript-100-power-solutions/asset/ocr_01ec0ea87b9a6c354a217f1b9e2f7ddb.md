# Chapter 10: Audio and Visual Effects 305

```
Billboard('billb', objects, 1, 500, 3000)
}
</script>
```

I laid out the HTML so that you can clearly see the three subobjects within the main containing object (with the ID 'billb'), which has its style display attribute set to 'hidden' so not to show the subobjects.
in the <script> section, the containing object is given a solid 1-pixel border (which is not necessary but improves the look) and resized to 320 by 100 pixels. The subobjects are then resized to those dimensions so that all elements are the same, then Show() is called to re-enable the displaying of the container div, and the Billboard() plug-in is attached to start things.
Next the mouseover and mouseout events of 'billb' are attached to the functions pause() and resume(). The pause() only needs to pass the arguments of 'billb' to reference the container object and the value 'stop' in the wait argument. In this instance, all other arguments will be ignored, they have been set to the empty string. resume() function, however, would be identical to the initial call made to start the billboard in the first place.

As you pass over the billboard it will stop, but it will resume once you move it away. Of course, the objects in this example are not linked to anything, but you will probably use this plug-in for advertising and make them clickable; you can even include forms within the.

> NOTE To place all the subobjects in the same location, they must start off lined underneath each other in the browser. In the case of divs, this will already be the case, but spans and images require a <br /> tag placed after them to ensure the correct positioning. The Billboard() plug-in subtracts the height of all previous objects to place each consecutive over the first. Should you forget to line them all this way, some of the objects will not display correctly, if at all.

# The Plug-in

```
function Billboard(id, objects, random, msecs, wait)
{
  var len = objects.length
  if (!O(id).BB_Ready)
{
    var h = 0
    O(id).BB_Index = 0
    O(id).BB_Ready = true
    FadeOut(objects.slice(1), 1, 0)

    for (j = 1; j < len; j++) {
      h = H(O(objects[j-1]))
```