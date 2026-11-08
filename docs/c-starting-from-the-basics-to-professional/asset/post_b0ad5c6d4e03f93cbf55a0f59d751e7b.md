
## TABLE OF CONTENTS

- Constant Pointers and Pointers to Constants ... 202
  - Pointer Arithmetic ... 205
  - Using Pointer Notation with an Array Name ... 208
- Dynamic Memory Allocation ... 210
  - The Stack and the Free Store ... 211
  - Using the new and delete Operators ... 212
  - Dynamic Allocation of Arrays ... 213
- Member Selection Through a Pointer ... 217
- Hazards of Dynamic Memory Allocation ... 218
  - Dangling Pointers and Multiple Deallocations ... 218
  - Allocation/Deallocation Mismatch ... 218
  - Memory Leaks ... 219
  - Fragmentation of the Free Store ... 219
- Golden Rule of Dynamic Memory Allocation ... 220
- Raw Pointers and Smart Pointers ... 221
  - Using `unique_ptr<T>` Pointers ... 222
  - Using `shared_ptr<T>` Pointers ... 225
- Understanding References ... 229
  - Defining References ... 229
  - Using a Reference Variable in a Range-Based for Loop ... 231
- Summary ... 232

### Chapter 7: Working with Strings ... 235

- A Better Class of String ... 235
  - Defining string Objects ... 236
  - Operations with String Objects ... 240
  - Accessing Characters in a String ... 244
  - Accessing Substrings ... 246
  - Comparing Strings ... 247
- Searching Strings ... 255
- Modifying a String ... 262
- `std::string` vs. `std::vector<char>` ... 267
- Converting Strings into Numbers ... 268
- Strings of International Characters ... 268
  - Strings of wchar_t Characters ... 269
  - Objects That Contain Unicode Strings ... 270
- Raw String Literals ... 271
- Summary ... 272

### Chapter 8: Defining Functions ... 275

- Segmenting Your Programs ... 275
  - Functions in Classes ... 276
  - Characteristics of a Function ... 276
- Defining Functions ... 276
  - The Function Body ... 279
  - Return Values ... 280
  - Function Declarations ... 281
- Passing Arguments to a Function ... 282
  - Pass-by-Value ... 283
  - Pass-by-Reference ... 291
- Default Argument Values ... 298
  - Multiple Default Parameter Values ... 299
- Arguments to main() ... 301
- Returning Values from a Function ... 302
  - Returning a Pointer ... 302
  - Returning a Reference ... 307
  - Returning vs. Output Parameters ... 307
  - Return Type Deduction ... 308
- Static Variables ... 310
- Function Overloading ... 311
  - Overloading and Pointer Parameters ... 313
  - Overloading and Reference Parameters ... 313
  - Overloading and const Parameters ... 315
  - Overloading and Default Argument Values ... 317
- Recursion ... 318
  - Basic Examples of Recursion ... 319
  - Recursive Algorithms ... 320
- Summary ... 327

### Chapter 9: Vocabulary Types ... 333

- Working with Optional Values ... 333
  - `std::optional` ... 335
- String Views: The New Reference-to-const-string ... 337
  - Using String View Function Parameters ... 339
  - A Proper Motivation ... 340
- Spans: The New Reference-to-vector or -array ... 340
  - Spans vs. Views ... 342
  - Spans of const Elements ... 342
  - Fixed-Size Spans ... 343
- Summary ... 344

### Chapter 10: Function Templates ... 347

- Function Templates ... 347
- Creating Instances of a Function Template ... 348
- Template Type Parameters ... 350
- Explicit Template Arguments ... 351
- Function Template Specialization ... 351
- Function Templates and Overloading ... 352
- Function Templates with Multiple Parameters ... 354
- Return Type Deduction in Templates ... 355
  - `decltype(auto)` ... 356
- Default Values for Template Parameters ... 357
- Non-Type Template Parameters ... 358
  - Templates for Functions with Fixed-Size Array Arguments ... 360
- Abbreviated Function Templates ... 362
  - Limitations to Abbreviated Function Templates ... 362
- Summary ... 363

### Chapter 11: Modules and Namespaces ... 365

- Modules ... 365
  - Your First Module ... 367
  - Export Blocks ... 369
  - Separating Interface from Implementation ... 370
  - Reachability vs. Visibility ... 375
  - Exporting Import Declarations ... 376
  - Managing Larger Modules ... 377
  - Global Module Fragments ... 381
- Namespaces ... 382
  - The Global Namespace ... 382
  - Defining a Namespace ... 383
  - Nested Namespaces ... 385
  - Namespaces and Modules ... 386
  - Functions and Namespaces ... 387
  - Using Directives and Declarations ... 389
  - Namespace Aliases ... 391
- Summary ... 391

### Chapter 12: Defining Your Own Data Types ... 395

- Classes and Object-Oriented Programming ... 395
  - Encapsulation ... 396
  - Inheritance ... 399
  - Polymorphism ... 400
- Terminology ... 402
- Defining a Class ... 402
  - Creating Objects of a Class ... 404
- Constructors ... 405
  - Default Constructors ... 405
  - Defining a Class Constructor ... 406
  - Using the default Keyword ... 408
  - Defining Functions Outside the Class ... 408
  - Default Arguments for Constructor Parameters ... 409
  - Using a Member Initializer List ... 410
  - Using the explicit Keyword ... 411
  - Delegating Constructors ... 413
  - The Copy Constructor ... 415
- Defining Classes in Modules ... 417
- Accessing Private Class Members ... 418
- The this Pointer ... 420
  - Returning this from a Function ... 421
- const Objects and const Member Functions ... 422
  - const Member Functions ... 423
  - const Correctness ... 425
  - Overloading on const ... 426
  - Casting Away const ... 427
  - Using the mutable Keyword ... 428
- Friends ... 429
  - The Friend Functions of a Class ... 429
  - Friend Classes ... 431
- Arrays of Class Objects ... 432
- The Size of a Class Object ... 434
- Static Members of a Class ... 434
  - Static Member Variables ... 435
  - Accessing Static Member Variables ... 438
  - Static Constants ... 438
