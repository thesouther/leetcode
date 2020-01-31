# leetcode34-在排序数组中查找元素的第一个和最后一个位置

给定一个按照升序排列的整数数组 `nums`，和一个目标值 `target`。找出给定目标值在数组中的开始位置和结束位置。

你的算法时间复杂度必须是 $O(log n)$ 级别。

如果数组中不存在目标值，返回 [-1, -1]。

示例 1:
```
输入: nums = [5,7,7,8,8,10], target = 8
输出: [3,4]
```
示例 2:
```
输入: nums = [5,7,7,8,8,10], target = 6
输出: [-1,-1]
```


### 题解

利用二分查找思想。

代码如下：

``` C++
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        vector<int> res;
        int start=-1,end=-1;
        int l=0;
        int r=nums.size() -1;
        while(l<=r){
            int mid = l+(r-l)/2;
            if(nums[mid]==target){
                start=end=mid;
                int sl=l;
                int sr=mid-1;
                int el=mid+1;
                int er=r;
                while(sl<=sr){
                    int smid=sl+(sr-sl)/2;
                    if(nums[smid]==target){
                        start=smid;
                        sr=smid-1;
                    }else{
                        sl=smid+1;
                    }
                }
                while(el<=er){
                    int emid=el+(er-el)/2;
                    // cout<<el<<er<<'\n';
                    // cout<<emid<<'\n';
                    if(nums[emid]==target){
                        end=emid;
                        el=emid+1;
                    }else{
                        er=emid-1;
                    }
                }
                break;
            }else if(nums[mid]>target){
                r=mid-1;
            }else{
                l=mid+1;
            }
        }
        res.push_back(start);
        res.push_back(end);
        return res;
    }
};

```