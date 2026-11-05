
- Section 54.3: PowerOf calculation 280
- Section 54.4: Recursively describe an object structure 280
- Section 54.5: Using Recursion to Get Directory Tree 281
- Section 54.6: Factorial calculation 284

## Chapter 55: Naming Conventions 285

- Section 55.1: Capitalization conventions 285
- Section 55.2: Enums 286
- Section 55.3: Interfaces 286
- Section 55.4: Exceptions 286
- Section 55.5: Private fields 287
- Section 55.6: Namespaces 287

## Chapter 56: XML Documentation Comments 288

- Section 56.1: Simple method annotation 288
- Section 56.2: Generating XML from documentation comments 288
- Section 56.3: Method documentation comment with param and returns elements 290
- Section 56.4: Interface and class documentation comments 290
- Section 56.5: Referencing another class in documentation 291

## Chapter 57: Comments and regions 292

- Section 57.1: Comments 292
- Section 57.2: Regions 292
- Section 57.3: Documentation comments 293

## Chapter 58: Inheritance 295

- Section 58.1: Inheritance. Constructors' calls sequence 295
- Section 58.2: Inheriting from a base class 297
- Section 58.3: Inheriting from a class and implementing an interface 298
- Section 58.4: Inheriting from a class and implementing multiple interfaces 298
- Section 58.5: Constructors In A Subclass 299
- Section 58.6: Inheritance Anti-patterns 299
- Section 58.7: Extending an abstract base class 300
- Section 58.8: Testing and navigating inheritance 301
- Section 58.9: Inheriting methods 301
- Section 58.10: Base class with recursive type specification 302

## Chapter 59: Generics 305

- Section 59.1: Implicit type inference (methods) 305
- Section 59.2: Type inference (classes) 306
- Section 59.3: Using generic method with an interface as a constraint type 306
- Section 59.4: Type constraints (new-keyword) 307
- Section 59.5: Type constraints (classes and interfaces) 308
- Section 59.6: Checking equality of generic values 309
- Section 59.7: Reflecting on type parameters 310
- Section 59.8: Covariance 310
- Section 59.9: Contravariance 311
- Section 59.10: Invariance 312
- Section 59.11: Variant interfaces 312
- Section 59.12: Variant delegates 313
- Section 59.13: Variant types as parameters and return values 314
- Section 59.14: Type Parameters (Interfaces) 314
- Section 59.15: Type constraints (class and struct) 315
- Section 59.16: Explicit type parameters 315
- Section 59.17: Type Parameters (Classes) 315
- Section 59.18: Type Parameters (Methods) 316
- Section 59.19: Generic type casting 316
- Section 59.20: Configuration reader with generic type casting 317

## Chapter 60: Using Statement

- Section 60.1: Using Statement Basics 319
- Section 60.2: Gotcha: returning the resource which you are disposing 320
- Section 60.3: Multiple using statements with one block 321
- Section 60.4: Gotcha: Exception in Dispose method masking other errors in Using blocks 322
- Section 60.5: Using statements are null-safe 322
- Section 60.6: Using Dispose Syntax to define custom scope 322
- Section 60.7: Using Statements and Database Connections 323
- Section 60.8: Executing code in constraint context 325

## Chapter 61: Using Directive

- Section 61.1: Associate an Alias to Resolve Conflicts 326
- Section 61.2: Using alias directives 326
- Section 61.3: Access Static Members of a Class 326
- Section 61.4: Basic Usage 327
- Section 61.5: Reference a Namespace 327
- Section 61.6: Associate an Alias with a Namespace 327

## Chapter 62: IDisposable interface

- Section 62.1: In a class that contains only managed resources 329
- Section 62.2: In a class with managed and unmanaged resources 329
- Section 62.3: IDisposable, Dispose 330
- Section 62.4: using keyword 330
- Section 62.5: In an inherited class with managed resources 331

## Chapter 63: Reflection

- Section 63.1: Get the members of a type 332
- Section 63.2: Get a method and invoke it 332
- Section 63.3: Creating an instance of a Type 333
- Section 63.4: Get a Strongly-Typed Delegate to a Method or Property via Reflection 336
- Section 63.5: Get a generic method and invoke it 337
- Section 63.6: Get a System.Type 338
- Section 63.7: Getting and setting properties 338
- Section 63.8: Create an instance of a Generic Type and invoke its method 338
- Section 63.9: Custom Attributes 339
- Section 63.10: Instantiating classes that implement an interface (e.g. plugin activation) 340
- Section 63.11: Get a Type by name with namespace 340
- Section 63.12: Determining generic arguments of instances of generic types 341
- Section 63.13: Looping through all the properties of a class 342

## Chapter 64: IQueryable interface

- Section 64.1: Translating a LINQ query to a SQL query 343

## Chapter 65: LINQ to Objects

- Section 65.1: Using LINQ to Objects in C# 344

## Chapter 66: LINQ Queries

- Section 66.1: Chaining methods 348
- Section 66.2: First, FirstOrDefault, Last, LastOrDefault, Single, and SingleOrDefault 349
- Section 66.3: Except 352
- Section 66.4: SelectMany 354
- Section 66.5: Any 355
- Section 66.6: JOINS 355
- Section 66.7: Skip and Take 358
- Section 66.8: Defining a variable inside a LINQ query (let keyword) 358
- Section 66.9: Zip 359
- Section 66.10: Range and Repeat 359
- Section 66.11: Basics 360
- Section 66.12: All 360
- Section 66.13: Aggregate 361
- Section 66.14: Distinct 362
- Section 66.15: SelectMany: Flattening a sequence of sequences 362
- Section 66.16: GroupBy 364
- Section 66.17: Query collection by type / cast elements to type 365
- Section 66.18: Enumerating the Enumerable 366
- Section 66.19: Using Range with various LINQ methods 367
- Section 66.20: Where 368
- Section 66.21: Using SelectMany instead of nested loops 368
- Section 66.22: Contains 368
- Section 66.23: Joining multiple sequences 370
- Section 66.24: Joining on multiple keys 372
- Section 66.25: ToLookup 372
- Section 66.26: SkipWhile 372
- Section 66.27: Query Ordering - OrderBy() ThenBy() OrderByDescending() ThenByDescending() 373
- Section 66.28: Sum 374
- Section 66.29: GroupBy one or multiple fields 374
- Section 66.30: OrderBy 375
- Section 66.31: Any and First(OrDefault) - best practice 376
- Section 66.32: GroupBy Sum and Count 376
- Section 66.33: SequenceEqual 377
- Section 66.34: ElementAt and ElementAtOrDefault 377
- Section 66.35: DefaultIfEmpty 378
- Section 66.36: ToDictionary 379
- Section 66.37: Concat 380
- Section 66.38: Build your own LINQ operators for IEnumerable<T> 380
- Section 66.39: Select - Transforming elements 381
- Section 66.40: OrderByDescending 382
- Section 66.41: Union 382
- Section 66.42: GroupJoin with outer range variable 383
- Section 66.43: LINQ Quantifiers 383
- Section 66.44: TakeWhile 383
- Section 66.45: Reverse 384
- Section 66.46: Count and LongCount 385
- Section 66.47: Incrementally building a query 385
- Section 66.48: Select with Func<TSource, int, TResult> selector - Use to get ranking of elements 387

## Chapter 67: LINQ to XML

- Section 67.1: Read XML using LINQ to XML 389

## Chapter 68: Parallel LINQ (PLINQ)

- Section 68.1: Simple example 391
- Section 68.2: WithDegreeOfParallelism 391
- Section 68.3: AsOrdered 391
- Section 68.4: AsUnordered 391

## Chapter 69: XmlDocument and the System.Xml namespace 392

- Section 69.1: XmlDocument vs XDocument (Example and comparison) 392
- Section 69.2: Reading from XML document 394
- Section 69.3: Basic XML document interaction 395

## Chapter 70: XDocument and the System.Xml.Linq namespace 396

- Section 70.1: Generate an XML document 396
- Section 70.2: Generate an XML document using fluent syntax 396
- Section 70.3: Modify XML File 397

## Chapter 71: C# 7.0 Features 399

- Section 71.1: Language support for Tuples 399
- Section 71.2: Local functions 403
- Section 71.3: out var declaration 404
- Section 71.4: Pattern Matching 405
- Section 71.5: Digit separators 407
- Section 71.6: Binary literals 407
- Section 71.7: throw expressions 408
- Section 71.8: Extended expression bodied members list 409
- Section 71.9: ref return and ref local 410
- Section 71.10: ValueTask<T> 411

## Chapter 72: C# 6.0 Features 413

- Section 72.1: Exception filters 413
- Section 72.2: String interpolation 417
- Section 72.3: Auto-property initializers 423
- Section 72.4: Null propagation 426
- Section 72.5: Expression-bodied function members 429
- Section 72.6: Operator nameof 431
- Section 72.7: Using static type 433
- Section 72.8: Index initializers 433
- Section 72.9: Improved overload resolution 435
- Section 72.10: Await in catch and finally 436
- Section 72.11: Minor changes and bugfixes 437
- Section 72.12: Using an extension method for collection initialization 437
- Section 72.13: Disable Warnings Enhancements 438

## Chapter 73: C# 5.0 Features 440

- Section 73.1: Async & Await 440
- Section 73.2: Caller Information Attributes 441

## Chapter 74: C# 4.0 Features 442

- Section 74.1: Optional parameters and named arguments 442
- Section 74.2: Variance 443
- Section 74.3: Dynamic member lookup 443
- Section 74.4: Optional ref keyword when using COM 444

## Chapter 75: C# 3.0 Features 445

- Section 75.1: Implicitly typed variables (var) 445
- Section 75.2: Language Integrated Queries (LINQ) 445
- Section 75.3: Lambda expressions 446
- Section 75.4: Anonymous types 446

## Chapter 76: Exception Handling 448

- Section 76.1: Creating Custom Exceptions 448
- Section 76.2: Finally block 450
