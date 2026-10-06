# Solutions to Chapter 7 | Object Oriented Design

7.9 Explain the data structures and algorithms that you would use to design an in-mem-ory file system. Illustrate with an example in code where possible.

# SOLUTION

For data block allocation, we can use bitmask vector and linear search (see "Practical File System-Design") or B+ trees (see Wikipedia).

```
struct DataBlock {
    char data[DATA_BLOCK_SIZE];
}
DataBlock dataBlocks[NUM_DATA_BLOCKS];
struct Inode { std::vector<int> databocks; };
struct Metadata {
    int size;
    Date last_modified, created;
    char extra_attributes;
};
std::vector<bool> dataBlockUsed(NUM_DATA_BLOCKS);
std::map<string, Inode *> mapFromName;
struct FSBase;
struct File : pubic FSBase {
    private:
    std::vector<Inode> * nodes;
    Metadata metaData;
};
structstruct Directory : pubic FSBase { std::vector<FSBase> * content; };
struct FileSystem {
    init();
    mount(FileSystem*);
    unmount(FileSystem* name) { ... };
     createFile(const char* name) { ... };
    Directory createDirectory(const char* name) { ... };
    // mapFromName to find Inode corresponding to file
    void openFile(File * file, FileMode mode) { ... };
    void close(File * file) { ... }
    void writeToFile(File * file, void * data, int num) { ... }
    void readFrom(File * file, void* res, int numbutes) { ... }
    int position) { ... }
};
```