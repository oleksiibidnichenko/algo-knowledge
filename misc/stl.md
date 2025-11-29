##  hash and unordered containers
### Hash Combine Function
```cpp
// based on boost::hash_combine
template <typename T>
inline void hash_combine(std::size_t& seed, const T& value) {
    std::hash hasher;
    seed ^= hasher(value) + 0x9e3779b9 + (seed << 6) + (seed >> 2);
}
```

### Custom hash function for std::pair (ditto for other types)
```cpp
struct PairHash {
    std::size_t operator()(const std::pair<int, int>& p) const {
        std::size_t seed = 0;
        hash_combine(seed, p.first);
        hash_combine(seed, p.second);
        return seed;
    }
};

// Declaration
std::unordered_map<std::pair<int, int>, std::string, PairHash> u_map;
```


##  priority_queue details
### Custom Comparator with operator()
```cpp
struct Ctx {
    int val;
    ... 
};

struct CtxCmp {
    bool operator()(const Ctx& l, const Ctx& r) const {
        // ">" for min heap, "<" for max heap
        return l.val > r.val;
    }
};

// Declaration
std::priority_queue<Ctx, std::vector<Ctx>, CtxCmp> p_q;
```

### Key Points
- **std::less<T>**: Creates max heap (default)
- **std::greater<T>**: Creates min heap
