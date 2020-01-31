# leetcode35-搜索插入位置

给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。

你可以假设数组中无重复元素。

**示例 1:**
```
输入: [1,3,5,6], 5
输出: 2
```

**示例 2:**
```
输入: [1,3,5,6], 2
输出: 1
```
**示例 3:**
```
输入: [1,3,5,6], 7
输出: 4
```

### 题解

二分查找法
（讲真，顺序查找效率不一定低）
``` C++
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int listLen = nums.size();
        int res = binarySearch(nums,target,0,listLen-1);
        return res;
    }
    int binarySearch(vector<int>& nums,int target, int start, int end){
        if(start==end){
            if(nums[start]>=target){
                return start;
            }else{
                start++;
                return start;
            }
        }
        int mid = (start+end)/2;
        if(nums[mid]==target){
            return mid;
        }else if(nums[mid]>target){
            return binarySearch(nums,target,start,mid);
        }else{
            return binarySearch(nums,target,mid+1, end);
        }
    }
};
```