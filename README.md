### 数组

#### 704. 二分查找
给定一个 n 个元素有序的（升序）整型数组 nums 和一个目标值 target  ，写一个函数搜索 nums 中的 target，如果目标值存在返回下标，否则返回 -1。
示例 1:

输入: nums = [-1,0,3,5,9,12], target = 9
输出: 4
解释: 9 出现在 nums 中并且下标为 4
示例 2:

输入: nums = [-1,0,3,5,9,12], target = 2
输出: -1
解释: 2 不存在 nums 中因此返回 -1

```java
class Solution {
    public int search(int[] nums, int target) {
        //暴力循环
        // for(int i = 0; i < nums.length; i++){
        //     if(nums[i] == target){
        //         return i;
        //     }
        // }

        //二分法
        int left = 0;
        int right = nums.length - 1;
        while(left <= right){
            int mid = (left + right) / 2;
            if(target == nums[mid]){
                return mid;
            } else if(target < nums[mid]){
                //目标值在左侧
                right = mid - 1;
            } else{
                //目标值在右侧
                left = mid + 1;
            }
        }

        //未找到目标值
        return -1;

    }
}
```


#### 27. 移除元素

给你一个数组 nums 和一个值 val，你需要 原地 移除所有数值等于 val 的元素。元素的顺序可能发生改变。然后返回 nums 中与 val 不同的元素的数量。

假设 nums 中不等于 val 的元素数量为 k，要通过此题，您需要执行以下操作：

更改 nums 数组，使 nums 的前 k 个元素包含不等于 val 的元素。nums 的其余元素和 nums 的大小并不重要。
返回 k。

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        //双指针
        int slow = 0;
        for(int fast = 0; fast < nums.length; fast++){
            if(nums[fast] != val){
                nums[slow] = nums[fast];
                slow++;
            }
        }
        return slow;

        /*
        用快指针在数组中寻找不等于目标值的数,赋值给慢指针
        相当于创建了一个新数组(慢指针),用快指针寻找不等于目标值的数,赋值给新数组
        如果快指针找到了不等于目标值的数,则慢指针后移一位
        */
    }
}
```

#### 977. 有序数组的平方

给你一个按 非递减顺序 排序的整数数组 nums，返回 每个数字的平方 组成的新数组，要求也按 非递减顺序 排序。

示例 1：

输入：nums = [-4,-1,0,3,10]
输出：[0,1,9,16,100]
解释：平方后，数组变为 [16,1,0,9,100]
排序后，数组变为 [0,1,9,16,100]
示例 2：

输入：nums = [-7,-3,2,3,11]
输出：[4,9,9,49,121]
 

提示：

1 <= nums.length <= 104
-104 <= nums[i] <= 104
nums 已按 非递减顺序 排序

```java
class Solution {
    public int[] sortedSquares(int[] nums) {
        //1.排序法
        // for(int i = 0; i < nums.length; i++){
        //     nums[i] = nums[i] * nums[i];

        // }
        // Arrays.sort(nums);
        // return nums;

        //2.双指针法
        int[] result = new int[nums.length];
        int k = result.length - 1;
        int left = 0;
        int right = nums.length - 1;
        while(left <= right){
            if(nums[left] * nums[left] >= nums[right] * nums[right]){
                result[k] = nums[left] * nums[left];
                k--;
                left++;
            } else {
                result[k] = nums[right] * nums[right];
                k--;
                right--;
            }

        }
        return result;
        /*
        创建一个新数组,创建一个指针指向新数组的最后
        创建两个指针,指向数组的两侧
        通过比较两侧的平方谁大,则赋值给新数组的最后一位,并且新数组的指针前移
        直到两个指针都指向同一个数停止
        */
    }
    
}
```


