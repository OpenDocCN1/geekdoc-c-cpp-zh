# FIGURE 7.8 Header File for the Linked-List Version of the Stack Template Class

# A Header File

```
// FILE: stack2.h (part of the namespace main_savitch_7B)
// See Figure 7.6 on page 370 for the other documentation that goes here.
// The only difference is that there is no CAPACITY constant.
//
// DYNAMIC MEMORY USAGE by the stack<Item> template class:
//   If there is insufficient dynamic memory, then the following functions throw bad_alloc:
//   the copy constructor, push, and the assignment operator.

#ifndef MAIN_SAVITCH_STACK2_H
#define MAIN_SAVITCH_STACK2_H
#include <cstddef>        // Provides NULL and size_t
#include "node2.h"        // Node template class from Figure 0.4 on page 326

namespace main_savitch_7B
{
    template <class Item>
    class stack
    {
    public:
        // TYPEDEFS
        typedef std::size_t size_type;
        typedef Item value_type;

        // CONSTRUCTORS and DESTRUCTOR
        stack( ) { top_ptr = NULL; }
        stack(const stack& source);
        ~stack( ) { list_clear(top_ptr); }
        // MODIFICATION MEMBER FUNCTIONS
        void push(const Item& entry);
        void pop( );
        void operator =(const stack& source);

        // CONSTANT MEMBER FUNCTIONS
        size_type size( ) const
        { return main_savitch_6B::list_length(top_ptr); }
        bool empty( ) const { return (top_ptr == NULL); }
        Item top( ) const;

    private:
        main_savitch_6B::node<Item> *top_ptr; // Points to top of stack
    };
}

#include "stack2.template" // Include the implementation
#endif
```