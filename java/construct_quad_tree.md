# [427. Construct Quad Tree](https://leetcode.com/problems/construct-quad-tree/)

## Approach 1: Recursive Division of Grid

### Solution
```java
// Time Complexity: O(n^2 * log n), where n is the side length of the grid
// Space Complexity: O(log n) (due to recursion stack)
public class Solution {
    public Node construct(int[][] grid) {
        return buildTree(grid, 0, 0, grid.length);
    }

    private Node buildTree(int[][] grid, int x, int y, int size) {
        if (size == 1) {
            // Base case: single cell
            return new Node(grid[x][y] == 1, true, null, null, null, null);
        }

        int halfSize = size / 2;

        // Recursively divide the grid into four quadrants
        Node topLeft = buildTree(grid, x, y, halfSize);
        Node topRight = buildTree(grid, x, y + halfSize, halfSize);
        Node bottomLeft = buildTree(grid, x + halfSize, y, halfSize);
        Node bottomRight = buildTree(grid, x + halfSize, y + halfSize, halfSize);

        // Check if all four quadrants are leaves with the same value
        if (topLeft.isLeaf && topRight.isLeaf && bottomLeft.isLeaf && bottomRight.isLeaf
                && topLeft.val == topRight.val && topRight.val == bottomLeft.val
                && bottomLeft.val == bottomRight.val) {
            return new Node(topLeft.val, true, null, null, null, null); // Merge into one leaf
        }

        // Otherwise, create an internal node
        return new Node(true, false, topLeft, topRight, bottomLeft, bottomRight);
    }
}
```