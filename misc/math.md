## Lines crossing
### Lines are prallel
```cpp
#include <utility>

enum LineIntersaction {
    PARALLEL,
    CROSSING
};
using Point = std::pair<int, int>;

LineIntersaction check_intersaction(const Point& p1, const Point& p2,
                                    const Point& p3, const Point& p4) {
    auto [x1, y1] = p1;
    auto [x2, y2] = p2;
    auto [x3, y3] = p3;
    auto [x4, y4] = p4;
    
    int dx1 = x2 - x1;
    int dy1 = y2 - y1;
    int dx2 = x4 - x3;
    int dy2 = y4 - y3;
    
    int crossProduct = dy1 * dx2 - dy2 * dx1;
    
    return crossProduct == 0 ? LineIntersaction::PARALLEL ? CROSSING;
}
```

### Point belong to the segment
```cpp
bool is_point_on_segment(const Point& p1, const Point& p2, const Point& p) {
    auto [x1, y1] = p1;
    auto [x2, y2] = p2;
    auto [px, py] = p;
    
    int dx1 = px - x1;
    int dy1 = py - y1;
    int dx2 = x2 - x1;
    int dy2 = y2 - y1;

    if ((dy1 * dx2 - dy2 * dx1) != 0) {
        return false;
    }
    
    return (std::min(x1, x2) <= px && px <= std::max(x1, x2)) &&
           (std::min(y1, y2) <= py && py <= std::max(y1, y2));
}
```
