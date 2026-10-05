# 13.3. FILE STREAMS

```
* v is a vector holding integers.
 */
void print_vector(const vector<int>& vec) {
    cout << "[";
    int len = vec.size();
    if (len > 0) {\n        for (int i = 0; i < len - 1; i++) {
            cout << vec[i] << ", "; // Comma between elements
        }
        cout << vec[len - 1]; // No comma after last element
    }
    cout << "]" << endl;
}
```

```
/
* save_vector(filename, v)
* Writes the contents of vector v.
* filename is name of text file created. Any file
* by name is overwritten.
* v is a vector holding integers.  v is unchanged by the
* function.
 */
void save_vector(const string& filename, const vector<int>& vec) {
    ofstream out;
    out.open(filename);
    if (out.good()) { // Make sure the file was opened properly
        int n = vec.size();
        for (int i = 0; i < n; i++) {
            out << vec[i] << " "; // Space delimited
        }
        out << endl;
        out.close();
    } else
        cout << "Unable to save the file" << endl;
```

```
/\n* load_vector(filename, v)
* Reads the contents of vector v from text file
* filename. v's contents are replaced by the file's
* contents. If the file cannot be found, the vector v
* is empty.
* v is a vector holding integers.
 */
void load_vector(const string& filename, vector<int>& vec) {
    ifstream in;
    in.open(filename);
    if (in.good()) { // Make sure the file was opened properly
        vec.clear(); // Start with empty vector
        int value;
        while (in >> value) // Read until end of file
            vec.push_back(value);
        }
        in.close();
    } else
        cout << "Unable to load in the file" << endl;
```