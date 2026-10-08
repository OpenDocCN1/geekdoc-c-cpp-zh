```
ifstream is {from);                   // input stream for file "from"
ofstream os (to);                    // output stream for file "to"

set<string> b {istream_iterator<string>{is},istream_iterator<string>{}}; // Il read input
copy(b,ostream_iterator<string>{os,"\n"});          // Il copy to output

return !is.eof() || !os;                            // return error state (§1.2.1, §11.4)
}
```