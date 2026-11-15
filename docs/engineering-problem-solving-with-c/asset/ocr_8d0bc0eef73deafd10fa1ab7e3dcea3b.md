Example:
friend Pixel operator +(Pixel, Pixel);

Prototype for friend function of overloaded << operator:
friend ostream& operator <<(ostream&, data type);

Example:
friend ostream& operator <<(ostream&, Pixel);

Prototype for friend function of overloaded >> operator:
friend istream& operator >>(istream&, data type&);

Example:
friend istream& operator >>(istream&, Pixel&);

Function prototypes for reading and writing binary data:
read(char* data, streamsize n);
write(char* data, streamsize n);

Opening binary files using ios::binary mode:
Example:
open(filename, ios::binary);

Class definition for public inheritance
class classname : public base class name

Example:
class Square : public Rectangle
{
public:
...
protected:
...
};

Specification of virtual methods
Prototype: virtual return data type function name (parameter list);
Example:
virtual void print(ostream&);

class Templates expression
Example:
template <typename identifier>

# Notes

+   1. Use constructors and member functions of the base class to assign values to inherited data members.