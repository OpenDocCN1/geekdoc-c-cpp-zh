# CHAPTER 9

# Introducing Types

# IN THIS CHAPTER

+   - Types Revisited 463
+   - Classes Versus Structs 466
+   - Type Members 486

Step by step, we're emerging from the cave of discrete language elements and starting to combine them into large programs. After our extensive coverage of expressions and statements, time has come to use them in a broader context. In this and the following few chapters, we lay the basis for “programming in the large,” exploring classes and structs as well as the various sorts of members they support.

In this chapter, we focus on the concept of types and contrast classes and structs. The discussion of a type's members is deferred until further chapters.

# Types Revisited

At the heart of managed code lies the concept of types. Defining the concept of a type is not an easy task, but put simply, it offers a means for the runtime to know what precisely a certain object is, and hence what the valid operations are to be performed on it. Typing is a crucial concept in the world of managed code because of the type-safety guarantees the platform offers.

Types are blueprints for objects. They describe the shape of objects that are said to have that particular type. Such a shape has two key elements:

+   - Data is what an object contains and operates on. It directly relates to the layout of objects in memory because storage needs to be provided for all the discrete pieces of data that make up an object.