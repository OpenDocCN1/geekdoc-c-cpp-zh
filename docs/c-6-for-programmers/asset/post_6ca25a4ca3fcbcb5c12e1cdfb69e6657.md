
- 6.10.1 Conditional AND (&&) Operator 143
- 6.10.2 Conditional OR (||) Operator 144
- 6.10.3 Short-Circuit Evaluation of Complex Conditions 145
- 6.10.4 Boolean Logical AND (&) and Boolean Logical OR (|) Operators 145
- 6.10.5 Boolean Logical Exclusive OR (^) 145
- 6.10.6 Logical Negation (!) Operator 146
- 6.10.7 Logical Operators Example 146

### 6.11 Wrap-Up 149

## 7 Methods: A Deeper Look 150

### 7.1 Introduction 151

### 7.2 Packaging Code in C# 152

### 7.3 static Methods, static Variables and Class Math 152
- 7.3.1 Math Class Methods 153
- 7.3.2 Math Class Constants PI and E 154
- 7.3.3 Why Is Main Declared static? 154
- 7.3.4 Additional Comments About Main 155

### 7.4 Methods with Multiple Parameters 155
- 7.4.1 Keyword static 157
- 7.4.2 Method Maximum 157
- 7.4.3 Assembling strings with Concatenation 157
- 7.4.4 Breaking Apart Large string Literals 158
- 7.4.5 When to Declare Variables as Fields 159
- 7.4.6 Implementing Method Maximum by Reusing Method Math.Max 159

### 7.5 Notes on Using Methods 159

### 7.6 Argument Promotion and Casting 160
- 7.6.1 Promotion Rules 161
- 7.6.2 Sometimes Explicit Casts Are Required 161

### 7.7 The .NET Framework Class Library 162

### 7.8 Case Study: Random-Number Generation 164
- 7.8.1 Creating an Object of Type Random 164
- 7.8.2 Generating a Random Integer 164
- 7.8.3 Scaling the Random-Number Range 165
- 7.8.4 Shifting Random-Number Range 165
- 7.8.5 Combining Shifting and Scaling 165
- 7.8.6 Rolling a Six-Sided Die 165
- 7.8.7 Scaling and Shifting Random Numbers 168
- 7.8.8 Repeatability for Testing and Debugging 168

### 7.9 Case Study: A Game of Chance; Introducing Enumerations 169
- 7.9.1 Method RollDice 172
- 7.9.2 Method Main's Local Variables 172
- 7.9.3 enum Type Status 172
- 7.9.4 The First Roll 173
- 7.9.5 enum Type DiceNames 173
- 7.9.6 Underlying Type of an enum 173
- 7.9.7 Comparing Integers and enum Constants 173

### 7.10 Scope of Declarations 174

### 7.11 Method-Call Stack and Activation Records 177
- 7.11.1 Method-Call Stack 177
- 7.11.2 Stack Frames 177
- 7.11.3 Local Variables and Stack Frames 178
- 7.11.4 Stack Overflow 178
- 7.11.5 Method-Call Stack in Action 178

### 7.12 Method Overloading 181
- 7.12.1 Declaring Overloaded Methods 181
- 7.12.2 Distinguishing Between Overloaded Methods 182
- 7.12.3 Return Types of Overloaded Methods 182

### 7.13 Optional Parameters 183

### 7.14 Named Parameters 184

### 7.15 C# 6 Expression-Bodied Methods and Properties 185

### 7.16 Recursion 186
- 7.16.1 Base Cases and Recursive Calls 186
- 7.16.2 Recursive Factorial Calculations 186
- 7.16.3 Implementing Factorial Recursively 187

### 7.17 Value Types vs. Reference Types 189

### 7.18 Passing Arguments By Value and By Reference 190
- 7.18.1 ref and out Parameters 191
- 7.18.2 Demonstrating ref, out and Value Parameters 192

### 7.19 Wrap-Up 194

## 8 Arrays; Introduction to Exception Handling 195

### 8.1 Introduction 196

### 8.2 Arrays 197

### 8.3 Declaring and Creating Arrays 198

### 8.4 Examples Using Arrays 199
- 8.4.1 Creating and Initializing an Array 199
- 8.4.2 Using an Array Initializer 200
- 8.4.3 Calculating a Value to Store in Each Array Element 201
- 8.4.4 Summing the Elements of an Array 202
- 8.4.5 Iterating Through Arrays with foreach 203
- 8.4.6 Using Bar Charts to Display Array Data Graphically; Introducing Type Inference with var 205
- 8.4.7 Using the Elements of an Array as Counters 207

### 8.5 Using Arrays to Analyze Survey Results; Intro to Exception Handling 208
- 8.5.1 Summarizing the Results 210
- 8.5.2 Exception Handling: Processing the Incorrect Response 211
- 8.5.3 The try Statement 211
- 8.5.4 Executing the catch Block 211
- 8.5.5 Message Property of the Exception Parameter 211

### 8.6 Case Study: Card Shuffling and Dealing Simulation 212
- 8.6.1 Class Card and Getter-Only Auto-Implemented Properties 212
- 8.6.2 Class DeckOfCards 213
- 8.6.3 Shuffling and Dealing Cards 215

### 8.7 Passing Arrays and Array Elements to Methods 216

### 8.8 Case Study: GradeBook Using an Array to Store Grades 219

### 8.9 Multidimensional Arrays 225
- 8.9.1 Rectangular Arrays 225
- 8.9.2 Jagged Arrays 226
- 8.9.3 Two-Dimensional Array Example: Displaying Element Values 227

### 8.10 Case Study: GradeBook Using a Rectangular Array 230

### 8.11 Variable-Length Argument Lists 236

### 8.12 Using Command-Line Arguments 237

### 8.13 (Optional) Passing Arrays by Value and by Reference 240

### 8.14 Wrap-Up 244

## 9 Introduction to LINQ and the List Collection 245

### 9.1 Introduction 246

### 9.2 Querying an Array of int Values Using LINQ 247
- 9.2.1 The from Clause 249
- 9.2.2 The where Clause 250
- 9.2.3 The select Clause 250
- 9.2.4 Iterating Through the Results of the LINQ Query 250
- 9.2.5 The orderby Clause 250
- 9.2.6 Interface IEnumerable<T> 251

### 9.3 Querying an Array of Employee Objects Using LINQ 251
- 9.3.1 Accessing the Properties of a LINQ Query's Range Variable 255
- 9.3.2 Sorting a LINQ Query's Results by Multiple Properties 255
- 9.3.3 Any, First and Count Extension Methods 255
- 9.3.4 Selecting a Property of an Object 255
- 9.3.5 Creating New Types in the select Clause of a LINQ Query 255

### 9.4 Introduction to Collections 256
- 9.4.1 List<T> Collection 256
- 9.4.2 Dynamically Resizing a List<T> Collection 257

### 9.5 Querying the Generic List Collection Using LINQ 261
- 9.5.1 The let Clause 263
- 9.5.2 Deferred Execution 263
- 9.5.3 Extension Methods ToArray and ToList 263
- 9.5.4 Collection Initializers 263

### 9.6 Wrap-Up 264

### 9.7 Deitel LINQ Resource Center 264

## 10 Classes and Objects: A Deeper Look 265

### 10.1 Introduction 266

### 10.2 Time Class Study; Throwing Exceptions 266
- 10.2.1 Time1 Class Declaration 267
- 10.2.2 Using Class Time1 268

### 10.3 Controlling Access to Members 270

### 10.4 Referring to the Current Object's Members with the this Reference 271

### 10.5 Time Class Case Study: Overloaded Constructors 273
- 10.5.1 Class Time2 with Overloaded Constructors 273
- 10.5.2 Using Class Time2's Overloaded Constructors 277

### 10.6 Default and Parameterless Constructors 279

### 10.7 Composition 280
- 10.7.1 Class Date 280
- 10.7.2 Class Employee 282
- 10.7.3 Class EmployeeTest 283

### 10.8 Garbage Collection and Destructors 284

### 10.9 static Class Members 284

### 10.10 readonly Instance Variables 288

### 10.11 Class View and Object Browser 289
- 10.11.1 Using the Class View Window 289
- 10.11.2 Using the Object Browser 290

### 10.12 Object Initializers 291

### 10.13 Operator Overloading: Introducing struct 291
- 10.13.1 Creating Value Types with struct 292
- 10.13.2 Value Type ComplexNumber 292
- 10.13.3 Class ComplexTest 294

### 10.14 Time Class Case Study: Extension Methods 295

### 10.15 Wrap-Up 298

## 11 Object-Oriented Programming: Inheritance 299

### 11.1 Introduction 300

### 11.2 Base Classes and Derived Classes 301

### 11.3 protected Members 303

### 11.4 Relationship between Base Classes and Derived Classes 304
- 11.4.1 Creating and Using a CommissionEmployee Class 305
- 11.4.2 Creating a BasePlusCommissionEmployee Class without Using Inheritance 309
- 11.4.3 Creating a CommissionEmployee-BasePlusCommissionEmployee Inheritance Hierarchy 314
- 11.4.4 CommissionEmployee-BasePlusCommissionEmployee Inheritance Hierarchy Using protected Instance Variables 317
- 11.4.5 CommissionEmployee-BasePlusCommissionEmployee Inheritance Hierarchy Using private Instance Variables 320

### 11.5 Constructors in Derived Classes 324

### 11.6 Software Engineering with Inheritance 324

### 11.7 Class object 325

### 11.8 Wrap-Up 326

## 12 OOP: Polymorphism and Interfaces 327

### 12.1 Introduction 328

### 12.2 Polymorphism Examples 330
