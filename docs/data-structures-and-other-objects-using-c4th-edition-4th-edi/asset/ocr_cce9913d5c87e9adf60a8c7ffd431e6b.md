# FIGURE 5.4 The Complete Node Class Definition

# A Class Definition

```
class node
{
public:
  // TYPEDEF
  typedef double value_type;
  // CONSTRUCTOR
  node(
     const value_type& init_data = value_type( ),
     node* init_link = NULL
     )
  { data_field = init_data; link_field = init_link; }
  // Member functions to set the data and link fields:
  void set_data(const value_type& new_data) { data_field = new_data; }
  void set_link(node* new_link) { link_field = new_link; }
  // Constant member function to retrieve the current data:
  value_type data( ) const { return data_field; }
  // Two slightly different member functions to retrieve the current link:
  const node* link( ) const { return link_field; }
  node* link( ) { return link_field; }
private:
  value_type data_field;
  node* link_field;
};
```

![](bbox=[0.12, 0.61, 0.24, 0.87])

# The Member Selection Operator

Suppose that a program has built the linked list shown in the margin. Now, head_ptr is a pointer to a node, so here is a small quiz: Using the dereferencing asterisk, what is the data type of *head_ptr? Remember that *head_ptr means “the thing that head_ptr points to.” Looking at the picture you can see that the data type of *head_ptr is a node.

As with any object, you can access the public member functions of *head_ptr. For example, the following writes the data (12.1) from the head node:

cout << (*head_ptr).data();

The expression (*head_ptr).data( ) means “activate the data member function of the node pointed to by head_ptr.” The parentheses are necessary around the first part of the expression, (*head_ptr), because the operation of accessing a member (such as the data member function) has higher precedence than the dereferencing asterisk. Without the parentheses, the