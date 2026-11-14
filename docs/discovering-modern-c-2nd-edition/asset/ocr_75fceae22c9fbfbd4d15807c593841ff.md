```
outfile.open("fb.txt", ios::binary);

double o1 = 5.2, o2 = 6.2;
outfile.write(reinterpret_cast<const char *>(&o1),
sizeof(o1));
outfile.write(reinterpret_cast<const char *>(&o2),
sizeof(o2));
outfile.close();

std::ifstream infile;
with_io_exceptions(infile);
infile.open("fb.txt", ios::binary);

double i1, i2;
infile.read(reinterpret_cast<char *>(&i1), sizeof(i1));
infile.read(reinterpret_cast<char *>(&i2), sizeof(i2));
std::cout << "i1 = " << i1 << ", i2 = " << i2 << "\n";
}
```

An advantage of binary I/O is that we do not need to worry about how the stream is parsed. On the other hand, non-matching types in the read and write commands result in completely unusable data. In particular, we must be utterly careful when the files are not read on the same platform as they were created: a long variable can contain 32 bits on one machine and 64 bits on another. For this purpose, the library <cstdint> provides types whose sizes are identical on every platform. The type int32_t, for instance, is a 32-bit signed int on every platform and uint32_t the corresponding unsigned.

The binary I/O works in the same manner for classes when they are self-contained, that is, when all data is stored within the object as opposed to external data referred to by pointers or references. Writing structures containing memory addresses—like trees or graphs—to files requires special representations since the addresses are obviously invalid in a new program run. In Section A.6.4, we will show a convenience function that allows us to write or read many objects in a single call.

Transferring data between different systems bears many risks in addition to the integer sizes mentioned above: numbers might be treated in different byte order (big endian vs. little endian) or members stored in a different order by another compiler. There are file formats and libraries—like Protobuf [70]—providing data portability.