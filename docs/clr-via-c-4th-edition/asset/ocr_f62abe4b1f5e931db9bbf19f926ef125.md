# # Serialization Surrogates

Up to now, I've been discussing how to modify a type's implementation to control how a type serializes and deserializes instances of itself. However, the formatters also allow code that is not part of the type's implementation to override how a type serializes and deserializes its objects. There are two main reasons why application code might want to override a type's behavior.

+   - It allows a developer the ability to serialize a type that was not originally designed to be serialized.
+   - It allows a developer to provide a way to map one version of a type to a different version of a type.

Basically, to make this mechanism work, you first define a "surrogate type" that takes over the actions required to serialize and deserialize an existing type. Then, you register an instance of your surrogate type with the formatter telling the formatter which existing type your surrogate type is responsible for acting on. When the formatter detects that it is trying to serialize or deserialize an instance of the existing type, it will call methods defined by your surrogate object. Let's build a sample that demonstrates how all this works.

A serialization surrogate type must implement the System.Runtime.Serialization.ISerializationSurrogate interface, which is defined in the FCL as follows.

```
    public interface ISerializationSurrogate {
        void GetObjectData(Object obj, SerializationInfo info, StreamingContext context);

        Object SetObjectData(Object obj, SerializationInfo info, StreamingContext context,
            ISurrogateSelector selector);
    }
```

Now, let's walk through an example that uses this interface. Let's say your program contains some DateTime objects that contain values that are local to the user's computer. What if you want to serialize the DateTime objects to a stream but you want the values to be serialized in universal time? This would allow you to send the data over a network stream to another machine in another part of the world and have the DateTime value be correct. Although you can't modify the DateTime type that ships with the FCL, you can define your own serialization surrogate class that can control how DateTime objects are serialized and deserialized. Here is how to define the surrogate class.

```
    internal sealed class UniversalToLocalTimeSerializationSurrogate : ISerializationSurrogate {
        public void GetObjectData(Object obj, SerializationInfo info, StreamingContext context) {
            // Convert the DateTime from local to UTC
            info.AddValue("Date", ((DateTime)obj).ToUniversalTime().ToString("u"));
        }

        public Object SetObjectData(Object obj, SerializationInfo info, StreamingContext context,
            ISurrogateSelector selector) {
            // Convert the DateTime from UTC to local
            return DateTime.ParseExact(info.GetString("Date"), "u", null).ToLocalTime();
        }
    }
```