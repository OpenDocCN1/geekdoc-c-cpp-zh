```
void with_io_exceptions(ios& io)
{   io.exceptions(ios_base::badbit | ios_base::failbit); }

int main ()
{
    std::::ofstream outfile;
    with_io_exceptions(outfile);
    outfile.open("f.txt");

    double o1= 5.2, o2= 6.2;
    outfile << o1 << o2 << std::endl; // no separation
    outfile.close();

    std::::ifstream infile;
    with_io_exceptions(infile);
    infile.open("f.txt");

    int i1, i2;
    char c;
    infile >> i1 >> c >> i2;   // mismatching types
    std::cout << "i1 = " << i1 << ", i2 = " << i2 << "\n";
}
```