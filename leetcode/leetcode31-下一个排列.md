# leetcode31-下一个排列

实现获取下一个排列的函数，算法需要将给定数字序列重新排列成字典序中下一个更大的排列。

如果不存在下一个更大的排列，则将数字重新排列成最小的排列（即升序排列）。

必须原地修改，只允许使用额外常数空间。

以下是一些例子，输入位于左侧列，其相应输出位于右侧列。

```
1,2,3 → 1,3,2
3,2,1 → 1,2,3
1,1,5 → 1,5,1
```

### 题解

索引i由后往前遍历数组，直到遇到某个数nums[i-1]<nums[i]，

如果不存在，则说明该排列为最大排列（逆序）,则将其顺序排序，变为最小排列；

如果存在，第i-1个数小于第i个数，则在i右边找到最小的大于第i-1个数的位置，记为j（要知道此时i右边的数字是逆序排列的，所以可以顺序找到位置j），交换i-1和j上的数字，此时i右边的数字还是逆序的，将其重排序为升序，即可得到下一个排列。

这里需要注意，在重排序时，因为i右边的数字们是降序的，所以将其重排序为升序时，只需要交换第一个和最后一个数字、第二个和倒数第二个数字，....，以此类推，节省排序时间。
代码如下：

``` C++
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        int listLen=nums.size();
        for(int i=listLen-1; i>0; i--){
            if(i==1 && nums[i-1]>nums[i]){
                resortList(nums, 0, listLen-1);
                break;
            }
            else if(nums[i-1] < nums[i]){
                int j=i-1;
                for(int j=listLen-1;j>i-1;j--){
                    if(nums[j]>nums[i-1]){
                        int k=nums[i-1];
                        nums[i-1]=nums[j];
                        nums[j]=k;
                        // swap(nums[j],nums[i-1]);
                        break;
                    }
                }
                // sort(nums.begin()+i,nums.end());
                resortList(nums,i,listLen-1);
                break;
            }
        }
        // return nums;
    }
    void resortList(vector<int>& nums, int start, int end){
        int k;
        while(start<end){
            int k=nums[start];
            nums[start]=nums[end];
            nums[end]=k;
            // swap(nums[start],nums[end]);
            start++;
            end--;
        }
    }
};
```