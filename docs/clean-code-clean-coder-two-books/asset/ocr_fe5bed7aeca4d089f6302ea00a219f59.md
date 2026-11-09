```
return String.format(“Could not find string parameter for -%c.”,
                    errorArgumentId);
case INVALID_INTEGER:
    return String.format(“Argument -%c expects an integer but was
’%s’.”,
                    errorArgumentId, errorParameter);
case MISSING_INTEGER:
    return String.format(“Could not find integer parameter for -%c.”,
                    errorArgumentId);
case INVALID_DOUBLE:
    return String.format(“Argument -%c expects a double but was ’%s’.”,
                    errorArgumentId, errorParameter);
case MISSING_DOUBLE:
    return String.format(“Could not find double parameter for -%c.”,
                    errorArgumentId);
case INVALID_ARGUMENT_NAME:
    return String.format(“‘%c” is not a valid argument name.”,
                    errorArgumentId);
case INVALID_ARGUMENT_FORMAT:
    return String.format(“%s” is not a valid argument format.”,
                    errorParameter);
}
return “”;
}

public enum ErrorCode {
    OK,        INVALID_ARGUMENT_FORMAT,
UNEXPECTED_ARGUMENT, INVALID_ARGUMENT_NAME,
    MISSING_STRING,
    MISSING_INTEGER, INVALID_INTEGER,
    MISSING_DOUBLE, INVALID_DOUBLE}
}
```

It’s remarkable how much code is required to flesh out the details of this simple concept. One of the reasons for this is that we are using a particularly wordy language. Java, being a statically typed language, requires a lot of words in order to satisfy the type system. In a language like Ruby, Python, or Smalltalk, this program is much smaller.¹