### The Concept

Instead of updating each element in the range directly (which would take O(n) time per update), we use a difference array to mark the boundaries of our updates.

### Algorithm Steps

1. **Create a difference array** `diff[]` of the same size as your original array, initialized to 0
2. **For each range update** [L, R] where you want to add value `val`:
   - `diff[L] += val` (mark the start)
   - `diff[R+1] -= val` (mark the end, if R+1 is within bounds)
3. **Build the final array** by computing the prefix sum of the difference array

### LeetCode problems
1. 370
