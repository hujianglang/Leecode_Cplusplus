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

具体题目如下：
（1）相关题目：

/*
拓展相关题目:给定范围求和：
Reference:   
https://www.cnblogs.com/grandyang/p/4952464.html

Range Sum Query - Immutable 区域和检索 - 不可变
Given an integer array nums, find the sum of the elements between indices iand j (i ≤ j), inclusive.

Example:

Given nums = [-2, 0, 3, -5, 2, -1]

sumRange(0, 2) -> 1
sumRange(2, 5) -> -1
sumRange(0, 5) -> -3

Note:

You may assume that the array does not change.
There are many calls to sumRange function.


这道题让我们检索一个数组的某个区间的所有数字之和，   
题目中给了两条条件，首先数组内容不会变化，
其次有很多的区间和检索。那么我们用传统的遍历相加来求  
每次区间和检索，十分的不高效，而且无法通过 OJ。  
所以这道题的难点就在于是否能想到来用建立累计直方图的思想来建立一个累计和的数组 dp，
其中 dp[i] 表示 [0, i] 区间的数字之和，那么 [i,j]  就可以表示为 dp[j]-dp[i-1]，这里要注意一下当 i=0 时，直接返回 dp[j] 即可，参见代码如下：
*/

```C++
//用小例子来帮助理解
class Solution1 {
public:
	NumArray(vector<int> &nums) {
		dp = nums;
		for (int i = 1; i < nums.size(); i++)
		{
			dp[i] += dp[i - 1];
		}
	}
	int sumRange(int i, int j) {
		return i == 0 ? dp[j] : dp[j] - dp[i - 1];
	}
private:
	vector<int> dp;
};
//当然，我们也可以通过增加一位 dp 的长度，来避免在 sumRange 中检测i是否为0，参见代码如下：
class Solution2 {
public:
	NumArray(vector<int> &nums) {
		dp.resize(nums.size() + 1,0);
		for (int i = 1; i <= nums.size(); ++i)
		{
			dp[i] = dp[i - 1] + nums[i - 1];
		}
		int sumRange(int i, int j) {
			return dp[j + 1] - dp[i];
		}
	}
private:
	vector<int> dp;
};
```




1，Maximum Sum Subarray of Size K (easy)  
Given an array nums and a target value k, find the maximum length of a  
subarray that sums to k. If there isn't one, return 0 instead.   
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
- ~~LinkedList Cycle (easy)~~
- Start of LinkedList Cycle (medium)
- Happy Number (medium)
- Middle of the LinkedList (easy)

/*
Reference:
https://www.cnblogs.com/grandyang/p/4355505.html
(1)Rotate List 旋转链表
Given a list, rotate the list to the right by k places, where k is non-negative.
For example:
Given 1->2->3->4->5->NULL and k = 2,
return 4->5->1->2->3->NULL.

这道旋转链表的题和之前那道 Rotate Array 旋转数组 很类似，但是比那道要难一些，
因为链表的值不能通过下表来访问，只能一个一个的走，  
我刚开始拿到这题首先想到的就是用快慢指针来解，
快指针先走k步，然后两个指针一起走，当快指针走到末尾时，  
慢指针的下一个位置是新的顺序的头结点，这样就可以旋转链表了，
还有就是当k大于链表长度和k远远大于链表长度时该如何处理，我们需要首先遍历一遍原链表得到链表长度n，
然后k对n取余，这样k肯定小于n，就可以用上面的算法了，代码如下:
*/

//Solution1 ：快慢指针
```C++
typedef struct ListNode
{
	int val;
	struct ListNode* next;
}ListNode;

class Solution1 {
public:
	ListNode* rotateRight(ListNode* head, int k) {
		if(!head) 
			return nullptr;
		int n = 0;
		ListNode* cur = head;
		while (cur) {
			++n;
			cur = cur->next;
		}

		k %= n;
		ListNode* fast = head, * slow = head;
		for (int i = 0; i < k; ++i)
			if (fast) fast = fast->next;
		if (!fast) return head;
		while (fast->next) {
			fast = fast->next;
			slow = slow->next;
		}
		fast->next = head;
		fast = slow->next;
		slow->next = nullptr;
		return fast;
	}
};
```

/*
这道题还有一种解法，跟上面的方法类似，但是不用快慢指针，一个指针就够了，
原理是先遍历整个链表获得链表长度n，然后此时把链表头和尾链接起来，
在往后走n - k % n个节点就到达新链表的头结点前一个点，这时断开链表即可，代码如下:
*/

```C++
class Solution2 {
public:
	ListNode* rotateRight(ListNode *head, int k) {
		if (!head) return nullptr;
		int n = 1;
		ListNode* cur = head;
		//此处没加到最后空，n=1已预先设置
		while (cur->next) {
			++n;
			cur = cur->next;
		}
		cur->next = head;
		int m = n - k % n;
		for (int i = 0; i < m; i++) {
			cur = cur->next;
		}
		ListNode* newHead = cur->next;
		cur->next = nullptr;
		return newHead;
	}
};
```

 
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

