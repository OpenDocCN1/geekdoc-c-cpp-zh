```
vector<char> vc(100); // elements of type char
int n;
cin>>n;
vc.resize(n); // make vc have n elements
```

Obviously, it is nice and useful to have **vectors** that allow this, but why is it important from a programming point of view? What makes it interesting to someone collecting useful programming techniques for future use? We are using two kinds of flexibility. We have a single entity, the **vector**, for which we can vary two things:

+   * The number of elements
* The type of elements

Those kinds of variability are useful in rather fundamental ways. We always collect data. Looking around my desk, I see piles of bank statements, credit card bills, and phone bills. Each of those is basically a list of information of various types: strings of letters and numeric values. In front of me lies a phone; it keeps lists of phone numbers and names. In the bookcases across the room, there is shelf after shelf of books. Our programs tend to be similar: we have containers of elements of various types. We have many different kinds of containers (**vector** is just the most widely useful), and they contain information such as phone numbers, names, transaction amounts, and documents. Essentially all the examples from my desk and my room originated in some computer program or another. The obvious exception is the phone: it *is* a computer, and when I look at the numbers on it I’m looking at the output of a program just like the ones we’re writing. In fact, those numbers may very well be stored in a **vector<Number>**.

Obviously, not all containers have the same number of elements. Could we live with a **vector** that had its size fixed by its initial definition; that is, could we write our code without **push_back()**, **resize()**, and equivalent operations? Sure we could, but that would put an unnecessary burden on the programmer: the basic trick for living with fixed-size containers is to move the elements to a bigger container when the number of elements grows too large for the initial size. For example, we could read into a **vector** without ever changing the size of a **vector** like this:

```
// read elements into a vector without using push_back:
vector<double>* p = new vector<double>(10);
int n = 0; // number of elements
for (double d; cin>>d; ) {
if (n==p->size()) {
vector<double>* q = new vector<double>(p->size()*2);
copy(p->begin(), p->end(), q->begin());
```