# 134. [Gas Station](https://leetcode.com/problems/gas-station/)

## Approach: Greedy Algorithm

### Solution
python
```python
# Time Complexity: O(n), where n is the number of gas stations
# Space Complexity: O(1)
class Solution:
    def canCompleteCircuit(self, gas, cost):
        totalGas = 0  # Total gas across all stations
        totalCost = 0  # Total cost across all stations
        startStation = 0  # Potential starting station
        currentGas = 0  # Gas balance while traversing

        for i in range(len(gas)):
            totalGas += gas[i]
            totalCost += cost[i]
            currentGas += gas[i] - cost[i]

            # If currentGas is negative, reset the starting station
            if currentGas < 0:
                startStation = i + 1
                currentGas = 0  # Reset gas balance

        # If total gas is less than total cost, completing the circuit is impossible
        return startStation if totalGas >= totalCost else -1
```
