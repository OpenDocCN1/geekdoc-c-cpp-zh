
## Before we get down to the code analysis, notice on line [3] the using namespace std construction. It opens the entire standard namespace of all standard headers that have been included in the currently compiled software, i.e. the translation unit. As a result, the std:: prefix can be omitted from the standard functions and classes. A downside is that a name clash can occur if there is already a function or a class with the same name as one in the opened namespace. So, the previous construction should be avoided, especially in header files. This means the std:: prefix should be explicitly used, especially if doing so does not diminish code readability. An alternative, also used in the majority of our examples, is to literally introduce each construction that we wish to use without the std:: prefix, such as using std::cout, using std::string, etc. Nevertheless, it is sometimes justified to open the entire std or other namespace in a source file (.cpp) that uses dozens of functions and classes from that namespace, if potential name clashes are well controlled (as in Functions_Lambdas.cpp, only a small fragment of which is shown in Listing 3.16). Our primary goal should be software correctness, and this and other rules should be chosen with care and applied only if they support this primary objective.

Our first lambda expression (a lambda function) is written entirely on line [11] in Listing 3.16. Compared with a “classical” function definition, instead of a name, it has a pair of square brackets: [ ]. Then, in parentheses, we see the definition of a formal parameter cm, followed by the function body in braces { }. Its role is simple – take the parameter cm, expressing centimeters, and convert it to inches by multiplying by 2.54. We mentioned that the lambda expression has no name; in many cases, there is no need to give a lambda a name. However, when necessary, the entire lambda expression can be assigned to an object, such as in our example on line [9]. This is a lambda closure object, which lets us make further references to that expression, such as the call on line [20]. Note, however, that there is no way to declare a type for this lambda closure object except using the auto keyword. At the end of this section, we will look further at this feature.

As shown in Figure 3.20, lambda expressions are composed of the following parts:

+   - **Caption** – Introduces external objects into the scope of the lambda
+   - **Formal arguments list** – A list of types and names defining formal arguments, as in any other function
+   - **Optional return type** – The -> operator followed by the type of the returned object
+   - **Lambda body** – A set of statements and expressions, including `return`, contained within braces { }

Each lambda includes a runtime object, called a lambda closure. If a lambda expression is attached to an identifier, it can be used to pass a function, like any other object, or to store it in an

![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_141_0.png)

**Figure 3.20** Lambda expressions are composed of three parts: caption, formal arguments list, and optional return type. The lambda body is contained within braces { }.

## Lines [18–20] should be straightforward, considering that the parameter o can represent any stream, such as std::cout, as well as an open file or a network port. To print out human-readable information, on line [21], text defined in the vector from line [16] is output.

Now we create a simple database with information about a few people taking a SCUBA diving course. This is represented by a vector named SCUBA_Class, containing StudentInfo objects:

```cpp
// Let us create a SCUBA class
vector<StudentInfo> SCUBA_Class {

    { L"Phil", L"Curtis",     18,   StudentInfo::SCUBA_Cert::kAdvanced },
    { L"Kamil", L"Cyganek",   15,   StudentInfo::SCUBA_Cert::kOpenWater },
    { L"John", L"Kowalski",   23,   StudentInfo::SCUBA_Cert::kOpenWater },
    { L"Michal", L"Brajta",   61,   StudentInfo::SCUBA_Cert::kInstructor },
    { L"Anna", L"McLachlan",  18,   StudentInfo::SCUBA_Cert::kAdvanced },
    { L"Boż", L"Cyganek",     49,   StudentInfo::SCUBA_Cert::kInstructor },
    { L"Megan", L"Plant",     26,   StudentInfo::SCUBA_Cert::kMaster }

};
```

Finally, in the following SCUBA_Course function, we display information about SCUBA students who fulfill certain conditions. First, the SCUBA_Class vector is sorted with the std::sort function, invoked on lines [43–44]. Since each StudentInfo object contains many data fields, we need to tell sort which one should be used for sorting. This is accomplished by providing sort with the lambda function defined on line [44]. It takes two constant references to StudentInfo objects and returns the Boolean value of a lexicographical comparison of fFamilyName strings. This does not require any further intervention since the compiler already “knows” how to compare strings. Then, on lines [47–48], the sorted vector is copied to the screen with the std::copy function (see Table 3.6).

Similar sorting and printing is done in the next few lines [54–59] of the function. However, this time we sort by fAge. Also, the auto keyword is used to automatically deduce the object types.

Finally, on line [65], std::copy_if is called: it outputs only those objects for which the fCert field is identical to the externally supplied cert object. This checking is done by another lambda function, defined on line [67]. However, unlike the two previous lambdas, this one uses a copy caption to bring cert into its scope:

```cpp
void SCUBA_Course( void )
{
    wcout << endl << L"Sorted by family name:" << endl;

    // -----------------------
    // Sort by family name
    sort( SCUBA_Class.begin(), SCUBA_Class.end(),
          [] ( const StudentInfo & a, const StudentInfo & b )
          { return a.fFamilyName < b.fFamilyName; } );

    // Print them on the screen
    copy( SCUBA_Class.begin(), SCUBA_Class.end(),
          ostream_iterator<StudentInfo, wchar_t> wcout, L"\n" );

    wcout << endl << L"Sorted by age:" << endl;

    // -----------------------
    // Sort by age
```

```cpp
sort( SCUBA_Class.begin(), SCUBA_Class.end(),
      [] ( const auto & a, const auto & b )
      { return a.fAge < b.fAge; } );

// Print them on the screen
copy( SCUBA_Class.begin(), SCUBA_Class.end(),
      ostream_iterator< StudentInfo, wchar_t >( wcout, L"\n" ) );

wcout << endl << L"Instructors in the group:" << endl;

// Find all with a given certificate
const auto cert = StudentInfo::SCUBA_Cert::kInstructor;
copy_if( SCUBA_Class.begin(), SCUBA_Class.end(),
         ostream_iterator< StudentInfo, wchar_t >( wcout, L"\n" ),
         [ cert ] ( const auto & a ) { return a.fCert == cert; } );

wcout << endl << endl;
}
```

When run, the program prints the following information about the SCUBA class:

```
Sorted by family name:
Michal Brajta,  61      Instructor
Phil Curtis,    18      Advanced
Kamil Cygánek,  15      OpenWater
Bog Cyganek,    49      Instructor
John Kowalski,  23      OpenWater
Anna McLaughlan, 18     Advanced
Megan Plant,    26      Master

Sorted by age:
Kamil Cygánek,  15      OpenWater
Phil Curtis,    18      Advanced
Anna McLaughlan, 18     Advanced
John Kowalski,  23      OpenWater
Megan Plant,    26      Master
Bog Cyganek,    49      Instructor
Michal Brajta,  61      Instructor

Instructors in the group:
Bog Cyganek,    49      Instructor
Michal Brajta,  61      Instructor
```

# What have we learned in this example?

+   - Lambda functions can be captioned by copy and by reference
+   - A simple `StudentInfo` structure holds personal information with the scoped, enumerated type `SCUBA_Cert`
+   - An overloaded stream insertion operator `<<` for `StudentInfo`
+   - The functions `std::sort` and `std::copy_if` from SL with supplied lambda functions and different captions

# 3.14.7  (✕) More on Lambda Functions

When using a lambda, it is very important is to properly specify the type of its caption. Examples of lambdas with different captions and various call conditions are shown in Table 3.10.
