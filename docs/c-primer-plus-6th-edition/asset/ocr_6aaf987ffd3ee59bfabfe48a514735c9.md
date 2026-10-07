template <class T, class Allocator = allocator<T> >
class vector {

If you omit a value for this template argument, the container template uses the
allocator<T> class by default. This class uses new and delete.

Listing 16.7 uses this class in an demanding application. This particular program cre-
ates vector objects, the one int specialization and one string specialization; each
has five elements.

# Listing 16.7 vect1.cpp

```
// vect1.cpp -- introducing the vector template
#include <iostream>
#include <string>
#include <vector>

const int NUM = 5;
int main()
{
  using std::vector;
  using std::string;
  using std::cin;
  using std::cout;
  using std::endl;

  vector<int> ratings(NUM);
  vector<string> titles(NUM);
  cout << "You will do exactly as told. You will enter\n"
    << NUM << " book titles and your ratings (0-10).\n";
  int i;
  for (i = 0; i < NUM; i++)
  {
    cout << "Enter title #" << i + 1 << ": ";
    getline(cin,titles[i]);
    cout << "Enter your rating (0-10): ";
    cin >> ratings[i];
    cin.get();
  }
  cout << "Thank you. You entered the following:\n"
    << "Rating\tBook\n";
  for (i = 0; i < NUM; i++)
  {
    cout << ratings[i] << "\t" << titles[i] << endl;
  }

  return 0;
}
```