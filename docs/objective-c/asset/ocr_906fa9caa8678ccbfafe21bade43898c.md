arbitrary dynamic data as well. This class is the NSData class. This class provides an object-oriented interface for a dynamically allocated byte buffer. You can use it to store any arbitrary chunk of bytes either directly or by copying the bytes from an allocated buffer. You can also use it to write that data out to disk as well.

# Using NSValue and NSNumber

Now that I’ve introduced you to each of these classes, in the next sections, I show you how to use them. I start with the NSValue and NSNumber classes, and then proceed on to NSData and NSMutabl eData.

# Wrapping arbitrary datatypes with NSValue

I mentioned before that NSValue is used for storing arbitrary data types. To create an NSValue, you provide it with a pointer to the value that you want to store, and a C string indicating the data type. Telling the NSValue instance about the type of the data is important because that tells it how many bytes it needs to read in order to get all of the data. Fortunately, Objective-C provides a special directive, @encode() that returns the appropriate encoding for a given type for your platform. Listing 14.1 shows how to create an NSValue using an arbitrary structure, passing the address of the structure instance for the pointer to the value, and using the @encode() directive to find the appropriate datatype.

Listing 14.1

# Creating an NSValue for an arbitrary structure

```
typedef struct
{
    int someMember;
    float someOtherMember;
} MyDataType;

MyDataType item;
item.someMember = 10;
item.someOtherMember = 500.3;
NSValue *boxedStruct = [NSValue value:&item
    withObjCType:@encode(MyDataType)];
```