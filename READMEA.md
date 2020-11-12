# LeetCode刷题指南
## 1. Pattern: Sliding window，滑动窗口类型
### 经典题目：
- ~~Maximum Sum Subarray of Size K (easy)~~
- Smallest Subarray with a given sum (easy)
- Longest Substring with K Distinct Characters (medium)
- Fruits into Baskets (medium)
- No-repeat Substring (hard)
- Longest Substring with Same Letters after Replacement (hard)
- Longest Subarray with Ones after Replacement (hard)

具体题目：
1，Maximum Sum Subarray of Size K (easy)
Given an array nums and a target value k, find the maximum length of a subarray that sums to k. If there isn't one, return 0 instead.
Example 1:
Given nums = [1, -1, 5, -2, 3], k = 3,
return 4. (because the subarray [1, -1, 5, -2] sums to 3 and is the longest)
Example 2:
Given nums = [-2, -1, 2, 1], k = 1,
return 2. (because the subarray [-1, 2] sums to 1 and is the longest)
Follow Up:
Can you do it in O(n) time?

```C++
class Solution {
public:
	int maxSubArrayLen(vector<int>& nums, int k)
	{
		int sum = 0, res = 0;
		unordered_map<int, int> m;
		for (int i = 0; i < nums.size(); i++)
		{
			sum += nums[i];
			if (sum == k) res = i + 1;
			else if (m.count(sum - k))
				res = max(res, i - m[sum - k]);
			if (!m.count(sum))
				m[sum] = i;
		}
		return res;
	}
};
```
## 2. Pattern: two points, 双指针类型
经典题目：
- Pair with Target Sum (easy)
- Remove Duplicates (easy)
- Squaring a Sorted Array (easy)
- Triplet Sum to Zero (medium)
- Triplet Sum Close to Target (medium)
- Triplets with Smaller Sum (medium)
- Subarrays with Product Less than a Target (medium)
- Dutch National Flag Problem (medium)
 
## 3. Pattern: Fast & Slow pointers, 快慢指针类型
经典题目：
- LinkedList Cycle (easy)
- Start of LinkedList Cycle (medium)
- Happy Number (medium)
- Middle of the LinkedList (easy)
 
## 4. Pattern: Merge Intervals，区间合并类型
经典题目：
- Merge Intervals (medium)
- Insert Interval (medium)
- Intervals Intersection (medium)
- Conflicting Appointments (medium)
 
## 5. Pattern: Cyclic Sort，循环排序
经典题目：
- Cyclic Sort (easy)
- Find the Missing Number (easy)
- Find all Missing Numbers (easy)
- Find the Duplicate Number (easy)
- Find all Duplicate Numbers (easy)
 
## 6. Pattern: In-place Reversal of a LinkedList，链表翻转
经典题目：
- Reverse a LinkedList (easy)
- Reverse a Sub-list (medium)
- Reverse every K-element Sub-list (medium)
 
##7. Pattern: Tree Breadth First Search，树上的BFS
经典题目：
- Binary Tree Level Order Traversal (easy)
- Reverse Level Order Traversal (easy)
- Zigzag Traversal (medium)
- Level Averages in a Binary Tree (easy)
- Minimum Depth of a Binary Tree (easy)
- Level Order Successor (easy)
- Connect Level Order Siblings (medium)
 
## 8. Pattern: Tree Depth First Search，树上的DFS
经典题目：
- Binary Tree Path Sum (easy)
- All Paths for a Sum (medium)
- Sum of Path Numbers (medium)
- Path With Given Sequence (medium)
- Count Paths for a Sum (medium)
 
## 9. Pattern: Two Heaps，双堆类型
经典题目：
- Find the Median of a Number Stream (medium)
- Sliding Window Median (hard)
- Maximize Capital (hard)
 
## 10. Pattern: Subsets，子集类型，一般都是使用多重DFS
经典题目：
- Subsets (easy)
- Subsets With Duplicates (easy)
- Permutations (medium)
- String Permutations by changing case (medium)
- Balanced Parentheses (hard)
- Unique Generalized Abbreviations (hard)
 
## 11. Pattern: Modified Binary Search，改造过的二分
经典题目：
- Order-agnostic Binary Search (easy)
- Ceiling of a Number (medium)
- Next Letter (medium)
- Number Range (medium)
- Search in a Sorted Infinite Array (medium)
- Minimum Difference Element (medium)
- Bitonic Array Maximum (easy)
 
## 12. Pattern: Top ‘K’ Elements，前K个系列
经典题目：
- Top ‘K’ Numbers (easy)
- Kth Smallest Number (easy)
- ‘K’ Closest Points to the Origin (easy)
- Connect Ropes (easy)
- Top ‘K’ Frequent Numbers (medium)
- Frequency Sort (medium)
- Kth Largest Number in a Stream (medium)
- ‘K’ Closest Numbers (medium)
- Maximum Distinct Elements (medium)
- Sum of Elements (medium)
- Rearrange String (hard)
 
## 13. Pattern: K-way merge，多路归并
经典题目：
- Merge K Sorted Lists (medium)
- Kth Smallest Number in M Sorted Lists (Medium)
- Kth Smallest Number in a Sorted Matrix (Hard)
- Smallest Number Range (Hard)
 
## 14. Pattern: 0/1 Knapsack (Dynamic Programming)，0/1背包类型
经典题目：
- 0/1 Knapsack (medium)
- Equal Subset Sum Partition (medium)
- Subset Sum (medium)
- Minimum Subset Sum Difference (hard)
 
## 15. Pattern: Topological Sort (Graph)，拓扑排序类型
经典题目：
- Topological Sort (medium)
- Tasks Scheduling (medium)
- Tasks Scheduling Order (medium)
- All Tasks Scheduling Orders (hard)
- Alien Dictionary (hard)

