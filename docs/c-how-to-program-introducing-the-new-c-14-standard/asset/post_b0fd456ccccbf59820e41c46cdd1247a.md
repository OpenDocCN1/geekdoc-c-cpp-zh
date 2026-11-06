
- 5.7.2 Class `DollarAmount` 175

### 5.8 `do ... while` Iteration Statement 179

### 5.9 `switch` Multiple-Selection Statement 180

### 5.10 `break` and `continue` Statements 186

- 5.10.1 `break` Statement 186
- 5.10.2 `continue` Statement 187

### 5.11 Logical Operators 188

- 5.11.1 Logical AND (`&&`) Operator 188
- 5.11.2 Logical OR (`||`) Operator 189
- 5.11.3 Short-Circuit Evaluation 190
- 5.11.4 Logical Negation (`!`) Operator 190
- 5.11.5 Logical Operators Example 191

### 5.12 Confusing the Equality (`==`) and Assignment (`=`) Operators 192

### 5.13 Structured-Programming Summary 194

### 5.14 Wrap-Up 199

## 6 Functions and an Introduction to Recursion 211

### 6.1 Introduction 212

### 6.2 Program Components in C++ 213

### 6.3 Math Library Functions 214

### 6.4 Function Prototypes 215

### 6.5 Function-Prototype and Argument-Coercion Notes 218

- 6.5.1 Function Signatures and Function Prototypes 219
- 6.5.2 Argument Coercion 219
- 6.5.3 Argument-Promotion Rules and Implicit Conversions 219

### 6.6 C++ Standard Library Headers 220

### 6.7 Case Study: Random-Number Generation 222

- 6.7.1 Rolling a Six-Sided Die 223
- 6.7.2 Rolling a Six-Sided Die 60,000,000 Times 224
- 6.7.3 Randomizing the Random-Number Generator with `srand` 225
- 6.7.4 Seeding the Random-Number Generator with the Current Time 227
- 6.7.5 Scaling and Shifting Random Numbers 227

### 6.8 Case Study: Game of Chance; Introducing Scoped `enums` 228

### 6.9 C++11 Random Numbers 232

### 6.10 Scope Rules 233

### 6.11 Function-Call Stack and Activation Records 237

### 6.12 Inline Functions 241

### 6.13 References and Reference Parameters 242

### 6.14 Default Arguments 245

### 6.15 Unary Scope Resolution Operator 247

### 6.16 Function Overloading 248

### 6.17 Function Templates 251

### 6.18 Recursion 254

### 6.19 Example Using Recursion: Fibonacci Series 257

### 6.20 Recursion vs. Iteration 260

### 6.21 Wrap-Up 263

## 7 Class Templates `array`s and `vector`; Catching Exceptions 283

### 7.1 Introduction 284

### 7.2 `array`s 284

### 7.3 Declaring `array`s 286

### 7.4 Examples Using `array`s 286

- 7.4.1 Declaring an `array` and Using a Loop to Initialize the `array`’s Elements 287
- 7.4.2 Initializing an `array` in a Declaration with an Initializer List 288
- 7.4.3 Specifying an `array`’s Size with a Constant Variable and Setting `array` Elements with Calculations 289
- 7.4.4 Summing the Elements of an `array` 290
- 7.4.5 Using a Bar Chart to Display `array` Data Graphically 291
- 7.4.6 Using the Elements of an `array` as Counters 292
- 7.4.7 Using `array`s to Summarize Survey Results 293
- 7.4.8 Static Local `arrays` and Automatic Local `arrays` 296

### 7.5 Range-Based `for` Statement 298

### 7.6 Case Study: Class `GradeBook` Using an `array` to Store Grades 300

### 7.7 Sorting and Searching `arrays` 306

- 7.7.1 Sorting 306
- 7.7.2 Searching 306
- 7.7.3 Demonstrating Functions `sort` and `binary_search` 306

### 7.8 Multidimensional `arrays` 307

### 7.9 Case Study: Class `GradeBook` Using a Two-Dimensional `array` 311

### 7.10 Introduction to C++ Standard Library Class Template `vector` 317

### 7.11 Wrap-Up 323

## 8 Pointers 339

### 8.1 Introduction 340

### 8.2 Pointer Variable Declarations and Initialization 341

- 8.2.1 Declaring Pointers 341
- 8.2.2 Initializing Pointers 342
- 8.2.3 Null Pointers Prior to C++11 342

### 8.3 Pointer Operators 342

- 8.3.1 Address (`&`) Operator 342
- 8.3.2 Indirection (`*`) Operator 343
- 8.3.3 Using the Address (`&`) and Indirection (`*`) Operators 344

### 8.4 Pass-by-Reference with Pointers 345

### 8.5 Built-In Arrays 349

- 8.5.1 Declaring and Accessing a Built-In Array 349
- 8.5.2 Initializing Built-In Arrays 350
- 8.5.3 Passing Built-In Arrays to Functions 350
- 8.5.4 Declaring Built-In Array Parameters 351
- 8.5.5 C++11: Standard Library Functions `begin` and `end` 351
- 8.5.6 Built-In Array Limitations 351
- 8.5.7 Built-In Arrays Sometimes Are Required 352

### 8.6 Using `const` with Pointers 352

- 8.6.1 Nonconstant Pointer to Nonconstant Data 353
- 8.6.2 Nonconstant Pointer to Constant Data 353
- 8.6.3 Constant Pointer to Nonconstant Data 354
- 8.6.4 Constant Pointer to Constant Data 355

### 8.7 `sizeof` Operator 356

### 8.8 Pointer Expressions and Pointer Arithmetic 358

- 8.8.1 Adding Integers to and Subtracting Integers from Pointers 359
- 8.8.2 Subtracting Pointers 360
- 8.8.3 Pointer Assignment 361
- 8.8.4 Cannot Dereference a `void*` 361
- 8.8.5 Comparing Pointers 361

### 8.9 Relationship Between Pointers and Built-In Arrays 361

- 8.9.1 Pointer/Offset Notation 362
- 8.9.2 Pointer/Offset Notation with the Built-In Array’s Name as the Pointer 362
- 8.9.3 Pointer/Subscript Notation 362
- 8.9.4 Demonstrating the Relationship Between Pointers and Built-In Arrays 363

### 8.10 Pointer-Based Strings (Optional) 364

### 8.11 Note About Smart Pointers 367

### 8.12 Wrap-Up 367

## 9 Classes: A Deeper Look 385

### 9.1 Introduction 386

### 9.2 `Time` Class Case Study: Separating Interface from Implementation 387

- 9.2.1 Interface of a Class 388
- 9.2.2 Separating the Interface from the Implementation 388
- 9.2.3 `Time` Class Definition 388
- 9.2.4 `Time` Class Member Functions 390
- 9.2.5 Scope Resolution Operator (`::`) 391
- 9.2.6 Including the Class Header in the Source-Code File 391
- 9.2.7 `Time` Class Member Function `setTime` and Throwing Exceptions 392
- 9.2.8 `Time` Class Member Function `toUniversalString` and String Stream Processing 392
- 9.2.9 `Time` Class Member Function `toStandardString` 393
- 9.2.10 Implicitly Inlining Member Functions 393
- 9.2.11 Member Functions vs. Global Functions 393
- 9.2.12 Using Class `Time` 394
- 9.2.13 Object Size 396

### 9.3 Compilation and Linking Process 396

### 9.4 Class Scope and Accessing Class Members 398

### 9.5 Access Functions and Utility Functions 399

### 9.6 `Time` Class Case Study: Constructors with Default Arguments 399

- 9.6.1 Constructors with Default Arguments 399
- 9.6.2 Overloaded Constructors and C++11 Delegating Constructors 404

### 9.7 Destructors 405

### 9.8 When Constructors and Destructors Are Called 405

- 9.8.1 Constructors and Destructors for Objects in Global Scope 406
- 9.8.2 Constructors and Destructors for Non-`static` Local Objects 406
- 9.8.3 Constructors and Destructors for `static` Local Objects 406
- 9.8.4 Demonstrating When Constructors and Destructors Are Called 406

### 9.9 Time Class Case Study: A Subtle Trap—Returning a Reference or a Pointer to a `private` Data Member 409

### 9.10 Default Memberwise Assignment 411

### 9.11 `const` Objects and `const` Member Functions 413

### 9.12 Composition: Objects as Members of Classes 415

### 9.13 `friend` Functions and `friend` Classes 421

### 9.14 Using the `this` Pointer 423

- 9.14.1 Implicitly and Explicitly Using the `this` Pointer to Access an Object’s Data Members 424
- 9.14.2 Using the `this` Pointer to Enable Cascaded Function Calls 425

### 9.15 `static` Class Members 429

- 9.15.1 Motivating Classwide Data 429
- 9.15.2 Scope and Initialization of `static` Data Members 429
- 9.15.3 Accessing `static` Data Members 430
- 9.15.4 Demonstrating `static` Data Members 430

### 9.16 Wrap-Up 433

## 10 Operator Overloading; Class `string` 447

### 10.1 Introduction 448

### 10.2 Using the Overloaded Operators of Standard Library Class `string` 449

### 10.3 Fundamentals of Operator Overloading 453

- 10.3.1 Operator Overloading Is Not Automatic 453
- 10.3.2 Operators That You Do Not Have to Overload 453
- 10.3.3 Operators That Cannot Be Overloaded 454
