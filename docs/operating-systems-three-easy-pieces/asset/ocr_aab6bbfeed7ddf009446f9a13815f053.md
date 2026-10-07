# File System Implementation

In this chapter, we introduce a simple file system implementation, known as **vsfs (the Very Simple File System)**. This file system is a simplified version of a typical UNIX file system and thus serves to introduce some of the basic on-disk structures, access methods, and various policies that you will find in many file systems today.

The file system is pure software; unlike our development of CPU and memory virtualization, we will not be adding hardware features to make some aspect of the file system work better (though we will want to pay attention to device characteristics to make sure the file system works well). Because of the greatest flexibility we have in building a file system, many different types have been built, literally from AFS (The Andrew File System) to ZFS (Sun's ZabbFS [B07]). All of these systems have different data structures and do things better or worse than their peers. Thus, the way we will be learning about file systems is through case studies: first, a simple file system (vsfs) in this chapter to introduce most concepts, and then a series of studies of real file systems to understand how they differ in practice.

> Crux: How to Implement A Simple File System How can we build a simple file system? What structures are on the disk? What do they need to track? How are they accessed?

# 4.1 The Way To Think

Thinking about file systems, we usually suggest thinking about two different aspects of them; if you understand both of these aspects, probably understand how the file system basically works.

The first is the **data structures** of the file system. In other words, what types of on-disk structures are utilized by the file system to organize its data and metadata. The first file systems we'll see (including vsfs below) employ simple structures, like arrays of blocks or other objects, whereas