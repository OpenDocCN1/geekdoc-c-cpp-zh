
```
[NSException exceptionWithName:@"Error opening file" reason:@"File doesn't exist." userInfo:nil];
}
else if(![self hasPermissionForFileAtPath:inPath])
{
    NSException *ex =
    [NSException exceptionWithName:@"Error opening file" reason:@"Permission error." userInfo:nil];
}
else
{
    NSException *ex =
    [NSException exceptionWithName:@"Error opening file" reason:@"Unknown error." userInfo:nil];
}
    @throw ex;
}
}
```

In this version of the -openFileAtPath: method, after I've determined that the file could not be opened, I then go through some of the typical reasons why it might have failed, and I craft an exception specifically to address each of those conditions. Once I have my exception built, I then throw the exception using the @throw directive.

In this particular case, I'm using the default NSException class to throw my exception. But if I wanted to be extra fancy, I could rewrite this method using a custom exception class for each of these different sorts of exceptional conditions.

An example of this is shown in Listing 10.4.

## Listing 10.4
### Throwing custom exceptions for different sorts of errors

```
-(void)openFileAtPath:(NSString *)inPath;
{
    contents =
        [[NSDictionary dictionaryWithContentsOfFile:inPath] retain];
    if(!contents)
```

## Listing 10.4 (continued)

```
{
    NSException *ex;
    if(![self fileExistsAtPath:inPath])
    {
        ex = [FileMissingException exceptionWithName:@"Error opening file" reason:@"File doesn't exist." userInfo:nil];
    }
    else if(![self hasPermissionForFileAtPath:inPath])
    {
        ex = [FilePermissionException exceptionWithName:@"Error opening file" reason:@"Permission error." userInfo:nil];
    }
    else
    {
        ex = [NSException exceptionWithName:@"Error opening file" reason:@"Unknown error." userInfo:nil];
    }
    @throw ex;
}
```

Notice that this method has had the return value removed completely. This is an example of code that returns successfully or not at all. In other words, if the file is able to be successfully opened, then the method returns successfully and everything works great. If an error occurs in opening the file, then an exception is thrown that will need to be caught by the caller.

## CAUTION

I can’t stress this enough, so I’ll make the point again here: In this code, if the exception gets thrown and it is not caught by someone up the stack from this method, then the application will crash. So clearly, you would only want to use an exception in this manner if you knew that the failure was a critical problem for this application.

Because it’s so important to catch these exceptions, take a look at how you do that. Listing 10.5 shows the updated main function for this application with proper exception handling code in place.

## Listing 10.5
### Handling the exception in the main function

```
int main (int argc, const char * argv[])
{
    int retCode = 0;
    @try
    {
        NSAutoreleasePool * pool = [[NSAutoreleasePool alloc] init];

        FileWrapper *wrapper = [[FileWrapper alloc] init];
        [wrapper openFileAtPath:@"..."];

        // do stuff with the file here...

    }
    @catch (NSException *e)
    {
        NSString *errorName = [e name];
        NSString *errorMsg = [e reason];
        NSLog(@"An error occurred: %@ - %@", errorName, errorMsg);
        retCode = -255;
    }
    @finally
    {
        [wrapper release];
        [pool drain];
    }
    return retCode;
}
```

The way that exceptions work enables them to actually interrupt program flow no matter where it is in your application and then jump up the stack until the exception is caught.

Therefore, when there is the possibility for an exception to occur in a method that you’re calling, you have to wrap the code that could throw an exception inside of what’s called a try/catch block. In the code shown above, you can see that one of the first things that this program does is to use the @try directive. This begins a try/catch block. Once you use the @try directive, the code inside of the following code block ( delimited by {} ) will be executed just like normal until it either reaches the end of the code block, or an exception is thrown.

If an exception is thrown, program flow is interrupted immediately, and it jumps to the exception handlers that are designated by the @catch directive.

The @catch directives allow you to catch exceptions of particular types. When an exception occurs, the code jumps to the @catch directives and looks for the closest match to the exception that has been thrown. It then begins executing again the code inside of the catch block.

In this particular case, the catch block is simply printing out the error message and then setting the applications return code to an error status. By catching the generic NSException, as shown in Listing 10.5, you are effectively catching all exceptions.

You could even catch the id data type instead of NSException. This would enable you to catch any object that’s thrown at all.

In cases like the earlier example where different kinds of exceptions are thrown for different kinds of error conditions, you would list separate catch blocks for each of the different kinds of exceptions that you needed to handle. An example of this is shown in Listing 10.6.

## Listing 10.6
### Catching different kinds of exceptions

```
int main (int argc, const char * argv[])
{
    int retCode = 0;
    @try
    {
        NSAutoreleasePool * pool = [[NSAutoreleasePool alloc] init];

        FileWrapper *wrapper = [[FileWrapper alloc] init];
        [wrapper openFileAtPath:@"..."];

        // do stuff with the file here...
    }
    @catch (FilePermissionException *e)
    {
        // ...
    }
    @catch (FileMissingException *e)
    {
        // ...
```

```
}
@catch (NSException *e)
{
    // ...
}
@finally
{
    [wrapper release];
    [pool drain];
}
return retCode;
}
```

When catching exceptions in this manner, you should list the exceptions in order from most specific to least specific, because the runtime will execute the first catch block match that it finds.

Because of the ability for an exception to interrupt program flow at any time, it can be difficult for your application to do appropriate cleanup of allocated memory and resources when an exception occurs. Fortunately, in addition to the try/catch constructs, there is an additional feature built into Objective-C exception handling, the @finally directive.

The @finally block works just like a @catch block except that it is always executed regardless of whether or not an exception occurs. This makes it the perfect place to clean up memory or free other resources that are allocated as part of the @try block. You can always rely on your @finally block being executed no matter what happens inside your try or catch blocks.

The advantages of this kind of error handling is that you can group your code and let it just run until something bad happens, and then handle that error condition. Additionally, errors can be very descriptive. You can put all sorts of things into the NSException object, and be as verbose as needed.

Try/catch/finally blocks can even be nested within each other in cases where you have complex processing requirements with complex error conditions. This allows you to have multiple levels of exception handling if needed.

## NOTE

The use of exceptions for error handling in Objective-C is relatively rare compared to some other languages that use exceptions much more extensively. If you’re coming from a language such as Java and are tempted to use exceptions yourself as extensively, I urge you to think twice, and instead, look at the next error handling mechanism that I’m going to visit, NSError.

## NOTE

To cause the debugger to break when an exception is thrown, you can set a breakpoint in the Objective-C runtime method objc_exception_throw. If you do this, when an exception is thrown, it will trigger your breakpoint and stop your application. You have to be careful though, since some methods will throw and catch an exception without allowing it to pass up the stack. This is normal, and doesn't hurt anything.

## Using NSError

When designing the Foundation framework, Apple recognized that they needed an error handling mechanism that retained the simplicity of a simple return code, but also provided a mechanism for specifying more information about what kind of error occurred. As a result, it began introducing a new error handling system called NSError. Listing 10.7 shows the file wrapper class, updated to use one.

## Listing 10.7
### File wrapper class using NSError

```
-(BOOL)openFileAtPath:(NSString *)inPath withError:(NSError **)outError;
{
    contents = [[NSDictionary dictionaryWithContentsOfFile:inPath] retain];
    if(!contents)
    {
        if(![self fileExistsAtPath:inPath])
        {
            NSDictionary *errorInfo =
            [NSDictionary dictionaryWithObject:@"File doesn't exist."
                                        forKey:NSLocalizedDescriptionKey];

            *outError = [NSError errorWithDomain:@"FileWrapper"
                                            code:404
                                        userInfo:errorInfo];
        }
        else if(![self hasPermissionForFileAtPath:inPath])
        {
            NSDictionary *errorInfo =
            [NSDictionary dictionaryWithObject:@"Permission Error."
                                        forKey:NSLocalizedDescriptionKey];

            *outError = [NSError errorWithDomain:@"FileWrapper"
                                            code:500
                                        userInfo:errorInfo];
```
