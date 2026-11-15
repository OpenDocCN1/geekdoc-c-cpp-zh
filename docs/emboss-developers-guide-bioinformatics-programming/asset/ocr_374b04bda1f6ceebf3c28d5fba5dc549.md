during ACD file processing but before the application proper starts, allowing for further fine control in the ACD file.

# 3.1.2.2 Support for common file formats

EMBOSS supports a wide range of file formats for input and output. Biological sequences can be read and written using all common formats. EMBOSS detects the format of an input sequence automatically, but this can be specified for efficiency. Many other formats for sequence features, alignments, data files and so on are handled automatically. Any application you write will support these formats automatically too. Furthermore, when new input and output data formats are added to EMBOSS, your applications will automatically be able to use them; no application code needs to change. For information on supported file formats, see the _EMBOSS User's Guide_.

# 3.1.2.3 Simple database configuration

Database configuration is simple and flexible. A variety of databases (which can include remote data servers) and diverse access methods are supported. New databases and access methods are easily added. For more information see the _EMBOSS Administrator's Guide_.

# 3.1.2.4 Command line handling

Your application will use the EMBOSS command line which is consistent across the applications. The ACD file defines the datatype and permissible values for all application options. The ACD file and all input at the command line is validated at startup, before the application proper starts. Command line behaviour, for example the production of a sensible prompt and reprompting for values that are out of range, is handled automatically.

# 3.1.2.5 Command line qualifiers

EMBOSS includes various command line qualifiers which are not (typically) set in an ACD file. These include _global qualifiers_ and various _datatype-specific qualifiers_. Global qualifiers are available to all applications and control general application behaviour. Datatype-specific qualifiers are used to specify particular inputs and outputs, for instance sequences, in more detail.

# 3.1.2.6 Sequence and sequence feature specification

Sequences are referenced on the command line by their Uniform Sequence Address (USA) which is a powerful and flexible specification for defining the location and format of sequence data. Similarly, sequence features are defined using a Uniform Feature Object (UFO). Any application you write will automatically support USAs and UFOs. For more information see the _EMBOSS User's Guide_.

# 3.1.3 Basic steps to development

There's more to software than just coding, especially when developing for EMBOSS which is widely distributed and deployed in production environments. All code that is to be integrated into the package must be tested, documented and managed throughout its lifetime. Regardless of whether you intend to develop the libraries or new applications, many of the steps are the same: