# Chapter 17

# Inheritance and Polymorphism

In Chapter 16 we saw how it is possible to design classes from which clients can produce objects that exhibit somewhat sophisticated behavior. The Rational, Stopwatch, LinkedList, and Tester classes were each built from scratch. C++ provides a way to create a class from an existing class by a process known as inheritance. Through this process the new class inherits all the characteristics of the existing class, and the class developer can extend and customize the inherited functionality as well as add new features.

# 17.1 I/O Stream Inheritance

Recall from Section 13.3 that writing to a file is almost as easy as printing on the screen. Once an ofstream object is set up, we can use the << operator in the same way we use it with the cout:

```
ofstream fout("myfile.dat");
int x = 10;
if (fout.good()) { // Make sure the file was opened properly
fout << "x = " << x << endl;
fout.close();
}
else
cout << "Unable to write to the file \"myfile.dat\" << endl;
```

Section 15.6 shows how operator<< may be overloaded for a programmer-defined type. For a type of vectors we can use the function

```
ostream operator<<(ostream& os, const vector<int>& vec) {
os << \'{, \';
int n = vec.size();
if (n > 0) { // Is the vector non-empty?
os << vec[0]; // Send first element to the stream
for (int i = 1; i < n; i++)
os << \', ' << vec[i]; // Send remaining elements
}
os << \';';
```