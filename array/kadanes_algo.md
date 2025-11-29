### The Concept

Instead of checking all possible subarrays (which would take O(n²) time), we use dynamic programming to
track the maximum sum ending at each position, keeping only the best result.

### Algorithm Steps

1. **Initialize two variables**:
   - `max_current` = first element (max sum ending at current position)
   - `max_global` = first element (best sum found so far)
2. **For each element** from index 1 to n-1:
   - `max_current = max(arr[i], max_current + arr[i])` (extend or start new)
   - `max_global = max(max_global, max_current)` (update best if needed)
3. **Return** `max_global` as the maximum subarray sum

### LeetCode problems
1. 53
