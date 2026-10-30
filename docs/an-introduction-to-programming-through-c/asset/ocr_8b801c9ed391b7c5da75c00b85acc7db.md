```
```cpp
class Literal : public Formula{
  string value;
public:
  Literal(string v){value=v;}
  void setSize(){
    width = textWidth(value);
    height = textHeight(); descent = height/2;
  }
  void draw(float clx, float cly){
    Text(clx+width/2,cly,value).imprint();
  }
};
```
```

This corresponds to the code for the case ’P’ in the corresponding functions on Node (Section ??).

We can now give a simple main program which can use the above definitions to render the formula $1 + \frac{1}{\frac{451}{5}+35}$.

```
```cpp
int main(){
  initCanvas("Formula drawing");

  Sum e(new Literal("1"),
        new Div(new Literal("2"),
                new Sum(new Div(new Literal("451"),new Literal("5")),
                        new Literal("35"))));

  e.setSize();
  e.draw(200,200+e.getHeight()-e.getDescent());

  getClick();
}
```
```

# 24.1.2 Comparison of the two approaches

At first glance, it might seem that the inheritance based approach is more verbose than the approach of Section 22.1. This is true, but the verbosity has bought us many things.

A key improvement is that we have partitioned the program into manageable pieces. The code of Section 22.1 had just one class. All the complexity was placed into that class. In contrast, in the new code, different concerns are separated into different classes. For example, the class Formula2a only models the fact that formulae can have two operands, nothing more. The class Formula2h shows how to layout formulae requiring horizontal layout. We can place each class into its header and implementation files, and the main program into a separate file, if we wish. This way, if we wish to change something regarding a certain issue (e.g. horizontal layout) we know that we will likely modify only one small file. This is a big benefit of the new approach.