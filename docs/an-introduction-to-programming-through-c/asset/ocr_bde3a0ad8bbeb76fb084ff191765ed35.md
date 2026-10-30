horizontal bar. Thus we get

d_{f/g} = d_g + a_g + h_o/2

a_{f/g} = d_f + a_f + h_o/2

Here h_o denotes the height needed to accommodate the horizontal bar.

As you can see, knowing the width, ascent, descent of f, g we can calculate the width, ascent, descent of f + g and also f/g. We will write this calculation as a recursive function setSizes. We will have members width, ascent, descent in each Node in which setSizes will store the values. So our structure becomes:

```
struct Node{
Node *lhs, *rhs;
char op;
string value;
double width, height, descent;
Node(string v);
Node(char op1, Node* lhs1, Node* rhs1);
Node(istream& infile);
void setSizes();
void draw(float clx, float y); // to actually draw
}
```

We have already given the implementations for the constructors. The implementation for setSizes follows the ideas described above. Note that f corresponds to lhs and g to rhs.

```
const double h_o = 20; // space for horizontal bar

void Node::setSizes(){
switch (op){
case 'p':            // Primitive formula
    width = textWidth(value);
    ascent = textHeight()/2; descent = textHeight()/2;
    break;
case '+':            // case f+g
    lhs->setSizes();
    rhs->setSizes();
    descent = max(lhs->descent, rhs->descent);
    width = lhs->width + textWidth(op) + rhs->width;
    ascent = max(lhs->ascent, rhs->ascent);
    break;
case '/':            // case f/g
    lhs->setSizes();
    rhs->setSizes();
    width = max(lhs->width, rhs->width);
    ascent = h_o/2 + lhs->ascent + lhs->descent;
```