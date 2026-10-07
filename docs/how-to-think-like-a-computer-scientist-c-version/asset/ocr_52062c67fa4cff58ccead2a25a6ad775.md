# CHAPTER 15. FILE INPUT/OUTPUT AND APMATRIX

might be a good idea to take the Set of city names and the apmatrix of distances, and combine them into a single object called a DistMatrix.

Here is a draft of what header for a DistMatrix might look like:

```
class DistMatrix {
private:
    Set cities;
    apmatrix<int> distances;
public:
    DistMatrix(int rows);
    void add (const apstring& city1, const apstring& city2, int dist);
    int distance (int i, int j) const;
    int distance (const apstring& city1, const apstring& city2) const;
    apstring cityName (int i) const;
    int numCities () const;
    void print ();
};
```

Using this interface simplifies main:

```
void main () {
    apstream line;
    ifstream infile("distances");
    DistMatrix distances (2);

    while (true) {
        getline(infile, line);
        if (infile.eof()) break;
        processLine (line, distances);
    }
    distances.print (
);
```

It also simplifies processLine:

```
void processLine(const apstring& line, DistMatrix& distances) {
    char quote = \"";
    apvector<int> quoteIndex(4);
    quoteIndex[0] = line.find(quote);
    for (int i=1; i<4; i++) {
        quoteIndex[i] = find (line, quote, quoteIndex[i-1]+1);
```