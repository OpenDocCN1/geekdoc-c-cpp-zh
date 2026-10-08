Standard C++.

11 See in the C++11 Chapter - Capturing a Class

12 To capture *this , the class has to be copyable. You can't use *this to capture a move-only class.

13 std::thread::hardware_concurrency() is a static member function which returns the number of concurrent threads supported by the implementation. Usually, it might be several hardware threads on a given system. On Wandbox it's 3, Coliru reports 4.

14 this appendix is based on a blog article available at https://www.bfilipek.com/2020/05/lambdasadvantages.html

15 You can use globals or static variables in a regular function, but it's not the best solution.