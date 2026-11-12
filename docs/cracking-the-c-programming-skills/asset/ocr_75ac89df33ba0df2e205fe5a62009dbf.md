```
catch (ifstream::failure& exObj) {
if (filePtr.rdstate() & ifstream::eofbit) {
cout << "End of file reached." << endl;
}
```

+   (a) When failbit is set, it generates it throws exception and prints "End of file reached"
+   (b) When End of file is reached, it throws exception and prints "End of file reached"
+   (c) a or b
+   (d) a and b

**Answer:** (c)

35. Say yes or no. Can we read the filename from an array of strings? (L1)
(a) Yes  (b) No

**Answer:** (a) Yes. We can create fstream/ifstream object from an array of file names.