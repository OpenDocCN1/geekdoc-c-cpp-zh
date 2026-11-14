![](bbox=[0.06, 0.07, 0.9, 0.33])

FIGURE 8.6 DCT blocks of Figure 8.3(a) with half of the blocks forced to zero, (b) resulting image from inverse DCT on each of these blocks.

appears as some blurred edges and loss of details. This is expected from a lossy compression methodology such as the one presented here.

# 8.6 ENTROPY CODING

After the data has been quantized into a finite set of values, it can be encoded using an entropy coder to give additional compression. By entropy, we mean the amount of information present in the data, and an entropy coder encodes the given set of symbols with the minimum number of bits required to represent them. Two of the most popular entropy coding schemes are Huffman coding and arithmetic coding. These techniques allocate variable-length codes for specific symbols (coefficient values in our case) in a set of values to be encoded. This saves even more space in terms of storage, thus adding to the compression.

# 8.7 JPEG COMPRESSION

Technically speaking, JPEG is not a file format at all; it is a compression method that is used in file formats such as TIFF and BMP, and the filename extension is .jpg or .jpeg. JPEG (pronounced “jay-peg”) gets its name from the committee that designed it, the Joint Photographic Experts Group. The key phrase here is photographic experts; this group was formed especially to design a better means of storing photographic and other photorealistic images. True color (24-bit color) was almost a given, so they concentrated on coming up with a good compression methodology. JPEG uses 24-bit