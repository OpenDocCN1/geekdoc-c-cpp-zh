For example, we could take our filesystem and add typed attributes by making the ResourceAttribute a polymodel. Then we could add sub-classes of ResourceAttribute for string attributes, integer attributes, and so on:

```
class ResourceAttribute(polymodel.PolyModel):
    name = db.StringProperty(required=True)

class StringAttribute(ResourceAttribute):
    strVal = db.StringProperty(required=True)

class IntegerAttribute(ResourceAttribute):
    intVal = db.IntegerProperty(required=True)
```

If you really must use an expando model, it's very simple—you make the class inherit from google.appengine.ext.db.Expando. In an expando model, you don't need to define the properties at all. You can define a set of fixed properties, which will be included in every instance of the model. But also, every field of the Python object will implicitly be treated as an untyped property. When you do this, you lose all of the help that datastore normally gives you. You don't get automatic references; you don't get any data validation. It's totally flexible and totally unstructured. You probably don't want to use it. I've yet to see an example of an expando model that really needed to be an expando. I'm not going to show you an example of one, because I can't think of any case where it really makes sense.

I could define a version of our filesystem that used an expando model. I could get rid of ResourceAttribute entirely and just use fields of the Python resource objects to store properties. But that would be a lousy solution. I'd lose the ability to define queries over attributes, and I'd lose a lot of structural consistency. What would I gain? Frankly, not much. I'd get a slightly better syntax for updating attributes, and that's really all.

# ### 14.3 Transactions, Keys, and Entity Groups

Back in Section **10.2, Storing Persistent Objects in GWT**, on page **145**, we talked about transactions, why they're so important, and how they work automatically in Java. It turns out that in Python, we've got transactions too, we just haven't bothered to look at them. Like lots of other things in App Engine with Python, the default behavior is set up so that most of the time, it's the right thing. But as usual, there will be