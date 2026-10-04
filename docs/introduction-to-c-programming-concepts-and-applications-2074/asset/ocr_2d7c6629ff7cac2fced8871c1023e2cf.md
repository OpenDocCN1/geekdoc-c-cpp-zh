You will use parallel vectors to store the product ID and the rating, similar to how you would handle an array. However, because you have vectors, you can add as many elements as you wish to the vector using push_back; you do not need to declare an array of particular size and read directly into it elements. You will compute the average rating by summing up you construct the vector and dividing by the total number (which you can get using the size command rather than having to store a value in an array data). Finally, you loop through the vector and output as you compare to the average; this final step is identical to how you would handle the problem with an array.

```
#include <iostream>
#include <vector>
using namespace std;
int main()
{
    vector<int> ID;
    vector<float> rating;
    float sumofratings = 0.0;
    int i;
    cout << "Enter a product ID and a rating, entering an ID of 0 to stop" << endl;
    int id;
    float r;
    cin >> id >> r;
    while (id > 0) { // Repeat until ID 0 is read in
        ID.push_back(id); // Store the product ID
        rating.push_back(r); // Store the product rating
        sumofratings += r; // Sum up ratings
        cin >> id >> r; // Read in next product
    }
    int totalnumber = ID.size();
    float averaging = sumofratings/totalnumber;
    cout << "The products with above average ratings are:" << endl;
    for(i=0;i<totalnumber;i++) {
        if (rating[i] > averaging) {
            cout << ID[i] << endl;
        }
    }
n}
```