# leetcode41-缺失的第一个正数

给定一个未排序的整数数组，找出其中没有出现的最小的正整数。

**示例1**:
```
输入: [1,2,0]
输出: 3
```

**示例2**:
```
输入: [3,4,-1,1]
输出: 2
```
**示例3**:
```
输入: [7,8,9,11,12]
输出: 1
```
**说明**:
 - 你的算法的时间复杂度应为O(n)，并且只能使用常数级别的空间。


### 题解

遍历一次数组把大于等于1的和小于数组大小的值放到原数组对应位置，然后再遍历一次数组查当前下标是否和值对应，如果不对应那这个下标就是答案，否则遍历完都没出现那么答案就是数组长度加1。

``` Python
class Solution:
    def firstMissingPositive(self, nums: List[int]) -> int:
        n=len(nums)
        res_list=[-1] * n
        # print(res_list)
        for i in range(n):
            if nums[i] >=1 and nums[i]<=n:
                res_list[nums[i]-1] =nums[i]
        # print(res_list)
        for i in range(n):
            if res_list[i] != i+1:
                return i+1
        return n+1
```