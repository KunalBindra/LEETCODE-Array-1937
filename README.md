# LEETCODE-Array-1937
Let's dry run the given code for the `maxPoints` method of the `Solution` class. The goal of this method is to compute the maximum number of points you can collect from a grid, where you can move in either direction in each row and can only move down to the next row.

### Code Breakdown
1. **Initialization**:
   ```java
   final int n = points[0].length;
   long[] dp = new long[n];
   ```
   Here, `n` represents the number of columns in each row of the `points` grid. `dp` is an array used to keep track of the maximum points collectable for each column of the current row.

2. **Iterating through each row**:
   ```java
   for (int[] row : points) {
   ```
   For each row in the `points` grid, the algorithm updates the `dp` array.

3. **Calculating left-to-right maximums**:
   ```java
   long[] leftToRight = new long[n];
   long runningMax = 0;
   for (int j = 0; j < n; ++j) {
     runningMax = Math.max(runningMax - 1, dp[j]);
     leftToRight[j] = runningMax;
   }
   ```
   This part calculates the maximum points you can collect if you are moving left-to-right in the current row.

4. **Calculating right-to-left maximums**:
   ```java
   long[] rightToLeft = new long[n];
   runningMax = 0;
   for (int j = n - 1; j >= 0; --j) {
     runningMax = Math.max(runningMax - 1, dp[j]);
     rightToLeft[j] = runningMax;
   }
   ```
   This part calculates the maximum points you can collect if you are moving right-to-left in the current row.

5. **Updating `dp` values for the current row**:
   ```java
   for (int j = 0; j < n; ++j)
     dp[j] = Math.max(leftToRight[j], rightToLeft[j]) + row[j];
   ```
   For each column, update `dp[j]` with the maximum value of points you can collect from either direction (left-to-right or right-to-left) plus the points at `row[j]`.

6. **Return the result**:
   ```java
   return Arrays.stream(dp).max().getAsLong();
   ```
   The maximum value in the `dp` array is returned, representing the maximum points collectable from the grid.

### Dry Run Example

Let's dry run the code with a sample input grid.

**Example Input:**
```java
int[][] points = {
  {1, 2, 3},
  {4, 5, 6},
  {7, 8, 9}
};
```

**Initial State:**
- `dp = [0, 0, 0]`

**Processing each row:**

1. **Row 1: [1, 2, 3]**
   - Left-to-right pass:
     - `runningMax = 0`, `leftToRight = [0, 0, 0]`
     - `leftToRight = [0, 0, 0]`
   - Right-to-left pass:
     - `runningMax = 0`, `rightToLeft = [0, 0, 0]`
     - `rightToLeft = [0, 0, 0]`
   - Update `dp`:
     - `dp = [1, 2, 3]`

2. **Row 2: [4, 5, 6]**
   - Left-to-right pass:
     - `runningMax = 0`, `leftToRight = [0, 0, 0]`
     - `leftToRight = [1, 2, 3]`
   - Right-to-left pass:
     - `runningMax = 0`, `rightToLeft = [0, 0, 0]`
     - `rightToLeft = [3, 3, 3]`
   - Update `dp`:
     - `dp = [5, 7, 9]`

3. **Row 3: [7, 8, 9]**
   - Left-to-right pass:
     - `runningMax = 0`, `leftToRight = [0, 0, 0]`
     - `leftToRight = [4, 6, 8]`
   - Right-to-left pass:
     - `runningMax = 0`, `rightToLeft = [0, 0, 0]`
     - `rightToLeft = [8, 8, 8]`
   - Update `dp`:
     - `dp = [12, 14, 17]`

**Result:**
- The maximum value in `dp` is `17`, which is the result returned by the method.

This dry run illustrates how the code works to compute the maximum number of points collectable. The use of `leftToRight` and `rightToLeft` arrays helps in efficiently calculating the maximum values considering movement in both directions.
