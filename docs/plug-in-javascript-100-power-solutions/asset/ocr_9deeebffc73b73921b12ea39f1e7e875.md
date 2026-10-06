# Chapter 3: The Core Plug-ins

```
window.onload = function() {
    alert (Htl('heading'))
    Htl('heading', '<h2>This is a subheading</h2>')
    alert (Htl('heading'))
}
<script>
```

The first section of HTML creates a div with <h1> heading. Then the <script> section immediately pops up an alert showing this value by using a call to Htl(). After, the value of the object's innerHTML property is changed to a subheading, again using Htl(), and then a second call to the JavaScript alert() function redplays the property, using the Htl() function—at each time you will see that the contents has changed.

# The Plug-in

```
function Htl(id, value) {
    if (typeof id != UNDEF) {
        O(id).innerHTML = value
    }
    return O(id).innerHTML
}
```

# SaveState()

After you change the properties for an object, there are times when you might want to restore it to its original state. This plug-in allows you to back up the most important style properties of an object. Figure 3-13 shows a div being prepared with a few values prior to testing the SaveState() plug-in.

# About the Plug-in

This plug-in backs up several of the most important style properties of an object, where they can be later retrieved should you need them. It takes the following argument:

+   - **id** The object properties are to be backed up

Figure 3-13 Creating a div with which to test saving and restoring states

![](bbox=[0.313, 0.737, 0.859, 0.931])