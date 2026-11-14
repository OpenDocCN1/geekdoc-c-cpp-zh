```
...: error: 'all_info' marked 'override' but doesn't override
any member functions
virtual void all_info() override {
^^^^^^^^^^^^^^^^^^^^
...: warning: 'student::all_info' hides overloaded virtual fct.
...: note: hidden overloaded virtual function 'person::all_info'
declared here: different qualifiers (const vs none)
virtual void all_info() const { ... }
^^^^^^^^^^^^^^^^^^^^
```