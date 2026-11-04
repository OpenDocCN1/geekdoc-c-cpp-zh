
- Strings Are Immutable ... 161
- Strings Can Be Used in switch Statements ... 162

## 8 A Closer Look at Methods and Classes ... 165
- Controlling Access to Class Members ... 165
  - C#'s Access Modifiers ... 165
  - Applying Public and Private Access ... 167
  - Controlling Access: A Case Study ... 168
- Pass References to Methods ... 172
  - How Arguments Are Passed ... 174
  - Use ref and out Parameters ... 176
    - Use ref ... 177
    - Use out ... 178
    - Use ref and out on References ... 181
  - Use a Variable Number of Arguments ... 182
- Return Objects ... 185
- Return an Array ... 187
- Method Overloading ... 188
  - Overload Constructors ... 194
  - Invoke an Overloaded Constructor Through this ... 197
  - Object Initializers ... 199
- The Main( ) Method ... 200
  - Return Values from Main( ) ... 200
  - Pass Arguments to Main( ) ... 200
- Recursion ... 202
- Understanding static ... 205
  - Static Constructors ... 210
  - Static Classes ... 211

## 9 Operator Overloading ... 213
- Operator Overloading Fundamentals ... 213
  - Overloading Binary Operators ... 214
  - Overloading Unary Operators ... 216
  - Handling Operations on C# Built-in Types ... 220
  - Overloading the Relational Operators ... 224
  - Overloading true and false ... 226
  - Overloading the Logical Operators ... 229
    - A Simple Approach to Overloading the Logical Operators ... 229
    - Enabling the Short-Circuit Operators ... 231
- Conversion Operators ... 235
- Operator Overloading Tips and Restrictions ... 239
- Another Example of Operator Overloading ... 240

## 10 Indexers and Properties ... 245
- Indexers ... 245
  - Creating One-Dimensional Indexers ... 245
  - Indexers Can Be Overloaded ... 249
  - Indexers Do Not Require an Underlying Array ... 251
  - Multidimensional Indexers ... 252
- Properties ... 254
  - Auto-Implemented Properties ... 259
  - Use Object Initializers with Properties ... 260
  - Property Restrictions ... 261
  - Use Access Modifiers with Accessors ... 261
  - Using Indexers and Properties ... 264

## 11 Inheritance ... 269
- Inheritance Basics ... 269
- Member Access and Inheritance ... 272
  - Using Protected Access ... 275
- Constructors and Inheritance ... 276
  - Calling Base Class Constructors ... 278
- Inheritance and Name Hiding ... 282
  - Using base to Access a Hidden Name ... 283
- Creating a Multilevel Hierarchy ... 285
- When Are Constructors Called? ... 288
- Base Class References and Derived Objects ... 289
- Virtual Methods and Overriding ... 294
  - Why Overridden Methods? ... 297
  - Applying Virtual Methods ... 298
- Using Abstract Classes ... 301
- Using sealed to Prevent Inheritance ... 305
- The object Class ... 305
  - Boxing and Unboxing ... 307
  - Is object a Universal Data Type? ... 309

## 12 Interfaces, Structures, and Enumerations ... 311
- Interfaces ... 311
  - Implementing Interfaces ... 312
  - Using Interface References ... 316
  - Interface Properties ... 318
  - Interface Indexers ... 320
- Interfaces Can Be Inherited ... 322
- Name Hiding with Interface Inheritance ... 323
- Explicit Implementations ... 323
- Choosing Between an Interface and an Abstract Class ... 326
- The .NET Standard Interfaces ... 326
- Structures ... 326
  - Why Structures? ... 330
- Enumerations ... 332
  - Initialize an Enumeration ... 333
  - Specify the Underlying Type of an Enumeration ... 334
  - Use Enumerations ... 334

## 13 Exception Handling ... 337
- The System.Exception Class ... 337
- Exception Handling Fundamentals ... 338
  - Using try and catch ... 338
  - A Simple Exception Example ... 338
  - A Second Exception Example ... 340
  - The Consequences of an Uncaught Exception ... 341
  - Exceptions Let You Handle Errors Gracefully ... 343
  - Using Multiple catch Clauses ... 344
  - Catching All Exceptions ... 345
  - Nesting try Blocks ... 346
  - Throwing an Exception ... 347
  - Rethrowing an Exception ... 348
  - Using finally ... 349
- A Closer Look at the Exception Class ... 351
  - Commonly Used Exceptions ... 352
  - Deriving Exception Classes ... 354
  - Catching Derived Class Exceptions ... 358
  - Using checked and unchecked ... 360

## 14 Using I/O ... 363
- C#'s I/O Is Built Upon Streams ... 363
- Byte Streams and Character Streams ... 363
- The Predefined Streams ... 363
- The Stream Classes ... 364
  - The Stream Class ... 364
  - The Byte Stream Classes ... 365
  - The Character Stream Wrapper Classes ... 365
- Binary Streams ... 367
- Console I/O ... 367
  - Reading Console Input ... 367
  - Using ReadKey() ... 369
  - Writing Console Output ... 371
- FileStream and Byte-Oriented File I/O ... 371
  - Opening and Closing a File ... 372
  - Reading Bytes from a FileStream ... 374
  - Writing to a File ... 375
  - Using FileStream to Copy a File ... 376
- Character-Based File I/O ... 378
  - Using StreamWriter ... 378
  - Using a StreamReader ... 380
- Redirecting the Standard Streams ... 381
- Reading and Writing Binary Data ... 383
  - BinaryWriter ... 383
  - BinaryReader ... 384
  - Demonstrating Binary I/O ... 386
