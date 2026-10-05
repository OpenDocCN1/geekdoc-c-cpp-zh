You should already be familiar with the g++ gzpack.cpp -o
gzpack.x part. The remaining parameters are as follows:

+   - -lz
- -l means that a library should be linked. Here it is z for libz.

+   - -Llib
- -L specifies search paths for libraries; here libz.a is located in the zlib directory.

+   - -Izlib/include
- -I specifies search paths for header files; here zlib.h is located in the zlib/include directory.