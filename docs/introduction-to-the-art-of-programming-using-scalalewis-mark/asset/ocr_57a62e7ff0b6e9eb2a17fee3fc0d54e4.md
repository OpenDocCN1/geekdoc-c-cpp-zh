resulting collection will be an ArrayBuffer. This is not the behavior you have come to expect from Scala collections where these methods tend to return the same type they operate on. This happens because we did not write those methods and we are relying on the implementations in the Buffer supertype to provide them. The Buffer type defaults to giving back an ArrayBuffer so that is what we see here.

If the solution to this required rewriting all of the methods that return collections, it would greatly reduce the benefit of extending the Buffer trait. The Scala collections library has been designed so that this is not required, but getting these methods to return a different type is still a bit challenging. To make your collection really fit in with the main collections library, there are a few things that need to be done. Instead of just extending the Buffer type, we also extend the BufferLike type. The BufferLike trait is one of a number of traits that end in Like that can be used to add onto the libraries.

The BufferLike trait takes two parameters. One is the type of the collection and the other is the collection type. In this case, MutableSLList[A]. That second type of parameter tells it what should be returned for calls that create a new collection, such as filter and map. Beyond this, things get a bit more complex. We need to specify a way for these types to be built. For our code, this leads to inheriting from GenericTraversableTemplate, making a companion object that is a SeqFactory, and making our class inherit from Builder as well. Putting it all together, the changes look like this.

```
import collection.generic._

class MutableSLList[A] extends mutable.Buffer[A]
    with GenericTraversableTemplate[A,MutableSLList]
    with mutable.BufferLike[A,MutableSLList[A]]
    with mutable.Builder[A,MutableSLList[A]] {
...

override def companion: GenericCompanion[MutableSLList] = MutableSLList

def result() = this
...
}

object MutableSLList extends SeqFactory[MutableSLList] {
    implicit def canBuildFrom[A]: CanBuildFrom[MutableSLList[_], A, MutableSLList[A]] =
        new GenericCanBuildFrom[A]
    def newBuilder[A]: mutable.Builder[A, MutableSLList[A]] =
        new MutableSLList[A]
}
```

This begins to pull in aspects of the Scala language that are mainly important for library writers. As the goal of this book is not to turn you into a proficient Scala library writer, we will not be putting this type of functionality into future collections as it obfuscates the concepts that you should be learning.