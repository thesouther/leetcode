# leeetcode33-搜索旋转排序数组  

假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 `[0,1,2,4,5,6,7]` 可能变为 `[4,5,6,7,0,1,2]` )。

搜索一个给定的目标值，如果数组中存在这个目标值，则返回它的索引，否则返回 -1 。

你可以假设数组中不存在重复的元素。

你的算法时间复杂度必须是 $O(log n)$ 级别。

**示例1**:
```
输入: nums = [4,5,6,7,0,1,2], target = 0
输出: 4
```
**示例2**:
```
输入: nums = [4,5,6,7,0,1,2], target = 3
输出: -1
```

### 题解

二分法，边找旋转中心边判断target可能所在的位置（左半边还是右半边）

代码如下：

``` C++
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int Slen = nums.size();
        int l=0,r=Slen-1;
        while(l<=r){
            int mid=l+(r-l)/2;
            if(nums[mid]==target) return mid;
            if(nums[l]<nums[r]){
                if(nums[mid]>target){
                    r=mid-1;
                }else{
                    l=mid+1;
                }
            }else{
                if(nums[mid]>nums[r]){
                    if(nums[l]==target) return l;
                    if(nums[l]>target){
                        if(nums[r]<target) return -1;
                        if(nums[r]==target) return r;
                        l=mid+1;
                    }else{
                        if(nums[mid]>target){
                            r=mid-1;
                        }else{
                            l=mid+1;
                        }
                    }
                }else{
                    if(nums[r]==target) return r;
                    if(nums[r]<target){
                        if(nums[l]==target) return l;
                        if(nums[l]>target) return -1;
                        r=mid-1;
                    }else{
                        if(nums[mid]<target){
                            l=mid+1;
                        }else{
                            r=mid-1;
                        }
                    }
                }
            }
        }
        return -1;
    }
};
```