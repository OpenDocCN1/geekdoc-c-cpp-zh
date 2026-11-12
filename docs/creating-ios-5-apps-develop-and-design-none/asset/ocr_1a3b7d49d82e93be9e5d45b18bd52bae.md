```
```objectivec
forKey:(NSString*)kCGImagePropertyGPSDictionary];
// Fill the sub-dictionary.
[locationMetadata setObject:[NSNumber numberWithFloat:lat]
    forKey:(NSString*)kCGImagePropertyGPSLatitude];
[locationMetadata setObject:latRef
    forKey:(NSString*)kCGImagePropertyGPSLatitudeRef];
[locationMetadata setObject:[NSNumber numberWithFloat:lon]
    forKey:(NSString*)kCGImagePropertyGPSLongitude];
[locationMetadata setObject:lngRef
    forKey:(NSString*)kCGImagePropertyGPSLongitudeRef];
[locationMetadata
    setObject:[NSNumber numberWithFloat:
        location.horizontalAccuracy]
    forKey:(NSString*)kCGImagePropertyGPSDOP];
[locationMetadata
    setObject:[NSNumber numberWithFloat:location.altitude]
    forKey:(NSString*)kCGImagePropertyGPSAltitude];
[locationMetadata
    setObject:location.timestamp
    forKey:(NSString*)kCGImagePropertyGPSTimeStamp];
}
return metadata;
}
```
```

Here, we instantiate a sub-dictionary and fill it with our location information. We then add it to our main dictionary. That's it. We return the main dictionary and we're done.

There are many, many other image properties that you might want to add to your application. I'll also leave that as an optional homework assignment.