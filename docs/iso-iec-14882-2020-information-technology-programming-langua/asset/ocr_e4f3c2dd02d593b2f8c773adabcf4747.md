```
namespace std {
    template<class Key, class T, class Compare = less<Key>,
            class Allocator = allocator<pair<const Key, T>>>
    class multimap {
    public:
        // types
        using key_type            = Key;
        using mapped_type         = T;
        using value_type          = pair<const Key, T>;
        using key_compare         = Compare;
        using allocator_type      = Allocator;
        using pointer             = typename allocator_traits<Allocator>::pointer;
        using const_pointer       = typename allocator_traits<Allocator>::const_pointer;
        using reference           = value_type&;
        using const_reference     = const value_type&;
        using size_type           = implementation-defined; // see 22.2
        using difference_type     = implementation-defined; // see 22.2
        using iterator            = implementation-defined; // see 22.2
        using const_iterator      = implementation-defined; // see 22.2
        using reverse_iterator    = std::reverse_iterator<iterator>;
        using const_reverse_iterator = std::reverse_iterator<const_iterator>;
        using node_type           = unspecified;

        class value_compare {
            friend class multimap;
        protected:
            Compare comp;
            value_compare(Compare c) : comp(c) { }
        public:
            bool operator()(const value_type& x, const value_type& y) const {
                return comp(x.first, y.first);
            }
        };

        // 22.4.5.2, construct/copy/destroy
        multimap() : multimap(Compare()) { }
        explicit multimap(const Compare& comp, const Allocator& = Allocator());
        template<class InputIterator>
            multimap(InputIterator first, InputIterator last,
                     const Compare& comp = Compare(),
                     const Allocator& = Allocator());
        multimap(const multimap& x);
        multimap(multimap&& x);
        explicit multimap(const Allocator&);
        multimap(const multimap&, const Allocator&);
        multimap(multimap&&, const Allocator&);
        multimap(initializer_list<value_type>,
                 const Compare& = Compare(),
                 const Allocator& = Allocator());
        template<class InputIterator>
            multimap(InputIterator first, InputIterator last, const Allocator& a)
            : multimap(first, last, Compare(), a) { }
        multimap(initializer_list<value_type> il, const Allocator& a)
            : multimap(il, Compare(), a) { }
        ~multimap();
        multimap& operator=(const multimap& x);
        multimap& operator=(multimap&& x)
            noexcept(allocator_traits<Allocator>::is_always_equal::value &&
                     is_nothrow_move_assignable_v<Compare>);
        multimap& operator=(initializer_list<value_type>);
        allocator_type get_allocator() const noexcept;

        // iterators
        iterator        begin() noexcept;
```