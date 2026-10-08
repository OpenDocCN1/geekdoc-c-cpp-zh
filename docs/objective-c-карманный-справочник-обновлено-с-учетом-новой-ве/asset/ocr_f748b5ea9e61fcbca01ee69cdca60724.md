# Parsing Command-Line Arguments 217

It’s quite unusual to access arguments this way.
The simplest way of parsing command-line arguments, as we saw in the last chapter, is to use the NSArgumentDomain in NSUserDefaults. When an Objective-C program is started, the command-line arguments are all read and inserted into a dictionary, which is used by the defaults system.

This makes it very easy to provide a set of command-line arguments along with (configurable) default values. You never interact with the arguments directly when you use this approach. Instead, you ask the defaults system for a value for a key, and it returns something that may be from a persistent storage location or from the command line.

In the EtoFoundation framework, we provide an GetOptionsDictionary() function, which wraps the standard getopt() function. This provides an Objective-C way of using UNIX-style command-line arguments. You can use this if you are writing a UNIX-style tool in Objective-C. Otherwise, it is better to use the defaults system.