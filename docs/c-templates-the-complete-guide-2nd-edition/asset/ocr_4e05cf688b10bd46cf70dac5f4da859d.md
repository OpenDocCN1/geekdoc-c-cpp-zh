unwrapping the variant into its head and tail, as we did with tuples in Section 25.1.1 on page 576, but with a union rather than a class: Click here to view code image

# variant/variantstorageasunion.hpp

```
template<typename... Types>
union VariantStorage;

template<typename Head, typename... Tail>
union VariantStorage<Head, Tail...> {
Head head;
VariantStorage<Tail...> tail;
};

template<>
union VariantStorage<> {
};
```

Here, the union is guaranteed to have sufficient size and alignment to allow any one of the types in Types to be stored at any given time. Unfortunately, this union itself is fairly hard to work with, because most of the techniques we will use to implement Variant will use inheritance, which is not permitted for a union.

Instead, we opt for a low-level representation of the variant storage: a character array large enough to hold any of the types and with suitable alignment for any of the types, which we use as a buffer to store the active value. The VariantStorage class template implements this buffer along with a discriminator: Click here to view code image

# variant/variantstorage.hpp

```
#include <new> // for std::launder()

template<typename... Types>
class VariantStorage {
using LargestT = LargestType<Typelist<Types...>>;
alignas(Types...) unsigned char buffer[sizeof(LargestT)];
unsigned char discriminator = 0;
public:
unsigned char getDiscriminator() const { return discriminator; }
void setDiscriminator(unsigned char d) { discriminator = d; } void* getRawBuffer() { return buffer; }
const void* getRawBuffer() const { return buffer; }

template<typename T>
T* getBufferAs() { return std::launder(reinterpret_cast<T*>(buffer));
```