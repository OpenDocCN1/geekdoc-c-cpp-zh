The attribute values are the strings enclosed in double quotes and may be parsed during ACD file processing into some other type depending on the data definition in which they occur. For example, this defines a default value:

```
default: "5.0"
```

If the above appeared in the definition for a floating point number (float:) then it would be held internally as a floating point number.

# Example

wossname has a string input parameter (search) and the string definition has five attributes (parameter:, default:, information:, help: and knowntype:):

```
string: search
[
    parameter: "Y"
    default: ""
    information: "Text to search for, or blank to list all
    programs"
    help: "Enter a word or words here and a case-independent search
    for it will be made in the one-line documentation, group names and
    keywords of all of the EMBOSS programs. If no keyword is
    specified, all programs will be listed."
    knowntype: "emboss keyword"
]
```

# 4.3.2 Parameter naming conventions

The qualifier or parameter name (the command line flag) of an ACD data definition must be a lowercase alphanumerical string without whitespace characters. In theory it can be of any length. In practice, there are conventions (Section A.1, “Introduction to ACD syntax”), and it is strongly recommended that you follow them. In some cases a warning or error message will be generated during ACD processing (i.e. when the ACD file is parsed, typically after the application is run) if you do not.

For example, the conventional name for the sequence datatype (input sequence) is sequence or *sequence and for seqout (output sequence) is outseq or *outseq. In other words, where more than one instance of a datatype is specified in an ACD file, then the characters a, b, etc. can be prepended to the flag. For example, use asequence, bsequence, etc. where more than one sequence is specified, or aoutseq, boutseq, etc. where more than one sequence output stream is specified. You can see this in the matcher application, which takes two input sequences:

```
sequence: asequence
[
    parameter: "Y"
    type: "protein"
]
```