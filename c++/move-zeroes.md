# [LeetCode 283: Move Zeroes](https://leetcode.com/problems/move-zeroes/)

## Approaches:
1. [Brute Force with Extra Array](#brute-force-with-extra-array)
2. [Optimized In-place with Two Pointers](#optimized-in-place-with-two-pointers)

### Approach 1: Brute Force with Extra Array

#### Intuition:
The problem is to move all the zeroes in the array to the end while maintaining the relative order of non-zero elements. A simple and naive way to achieve this is to use an auxiliary array to first collect all the non-zero elements and then fill in the zeroes.

#### Steps:
- Create a new array of the same size as the input to store non-zero elements.
- Iterate through the original array and copy non-zero elements to the new array.
- Once all non-zero elements are placed, fill the remaining array with zeroes.
- Finally, copy the auxiliary array back to the original array.

#### Code:
```cpp
void moveZeroes(vector<int>& nums) {
    int n = nums.size();
    vector<int> result(n);
    int index = 0;

    // Collect all non-zero numbers in result
    for (int i = 0; i < n; ++i) {
        if (nums[i] != 0) {
            result[index++] = nums[i];
        }
    }

    // Fill with zeros at the end
    for (int i = index; i < n; ++i) {
        result[i] = 0;
    }

    // Copy back to original array
    for (int i = 0; i < n; ++i) {
        nums[i] = result[i];
    }
}
```

#### Complexity Analysis:
- **Time Complexity**: O(n), where n is the number of elements in the array. The array is traversed a constant number of times.
- **Space Complexity**: O(n), because of the use of an auxiliary array of the same size as the input.

### Approach 2: Optimized In-place with Two Pointers

#### Intuition:
Instead of using extra space, we can optimize space complexity by using the two-pointer technique. The idea is to keep track of the next position where a non-zero element should be placed using a slow pointer while iterating the array with a fast pointer.

#### Steps:
- Initialize a pointer `lastNonZeroFoundAt` to track the position of the last non-zero found.
- Traverse the array with a fast pointer. Upon encountering a non-zero, swap it with the element at `lastNonZeroFoundAt`.
- Increment the `lastNonZeroFoundAt` pointer every time a swap operation is made.

#### Code:
```cpp
void moveZeroes(vector<int>& nums) {
    int lastNonZeroFoundAt = 0;

    // Move all non-zero numbers to the beginning
    for (int i = 0; i < nums.size(); i++) {
        if (nums[i] != 0) {
            // Swap the current element with the last non-zero found position
            std::swap(nums[lastNonZeroFoundAt], nums[i]);
            lastNonZeroFoundAt++;
        }
    }
}
```

#### Complexity Analysis:
- **Time Complexity**: O(n), where n is the number of elements in the array. Each element is visited exactly once.
- **Space Complexity**: O(1), as we perform the entire operation in-place with constant extra space.

This approach minimizes memory usage and maintains a linear time complexity, making it optimal for this problem.
### Approach Name: Two-Pointer Technique Using stable_partition

### Intuition: We want to rearrange the elements of the array so that all non-zero elements are placed at the beginning, maintaining their relative order. Zero elements are moved to the end, preserving the relative order among them as well.
stable_partition is a useful STL algorithm that can partition a container based on a predicate while maintaining relative order.

### Steps:
		1.	Use the stable_partition function from <algorithm> to rearrange elements in the array.
	2.	Provide a lambda function as the predicate to check whether an element is non-zero (n != 0).
	3.	stable_partition ensures that the non-zero elements remain in their original relative order at the start of the array, and the zeroes are moved to the end.

 ### code: 
 #include <iostream>
#include <vector>
#include <algorithm> // For stable_partition

void moveZeroes(std::vector<int>& nums) {
stable_partition(nums.begin(),nums.end(),[](int n){return n!=0 ;} );
}
int main() {
    std::vector<int> nums = {0, 1, 0, 3, 12};
    moveZeroes(nums);
    for (int num : nums) {
        std::cout << num << " ";
    }
    return 0;
}
