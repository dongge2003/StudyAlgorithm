### 数组

#### 704. 二分查找
>给定一个 n 个元素有序的（升序）整型数组 nums 和一个目标值 target  ，写一个函数搜索 nums 中的 target，如果目标值存在返回下标，否则返回 -1。

>示例 1:
>>输入: nums = [-1,0,3,5,9,12], target = 9
输出: 4
解释: 9 出现在 nums 中并且下标为 4 

>示例 2:
>>输入: nums = [-1,0,3,5,9,12], target = 2
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

>给你一个数组 nums 和一个值 val，你需要 原地 移除所有数值等于 val 的元素。元素的顺序可能发生改变。然后返回 nums 中与 val 不同的元素的数量。
假设 nums 中不等于 val 的元素数量为 k，要通过此题，您需要执行以下操作：
更改 nums 数组，使 nums 的前 k 个元素包含不等于 val 的元素。nums 的其余元素和 nums 的大小并不重要。
返回 k。

>示例 1：
>>输入：nums = [3,2,2,3], val = 3
输出：2, nums = [2,2,_,_]
解释：你的函数函数应该返回 k = 2, 并且 nums 中的前两个元素均为 2。
你在返回的 k 个元素之外留下了什么并不重要（因此它们并不计入评测）。 

>示例 2：
>>输入：nums = [0,1,2,2,3,0,4,2], val = 2
输出：5, nums = [0,1,4,0,3,_,_,_]
解释：你的函数应该返回 k = 5，并且 nums 中的前五个元素为 0,0,1,3,4。
注意这五个元素可以任意顺序返回。
你在返回的 k 个元素之外留下了什么并不重要（因此它们并不计入评测）。

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

>给你一个按 非递减顺序 排序的整数数组 nums，返回 每个数字的平方 组成的新数组，要求也按 非递减顺序 排序。

>示例 1：
>>输入：nums = [-4,-1,0,3,10]
输出：[0,1,9,16,100]
解释：平方后，数组变为 [16,1,0,9,100]
排序后，数组变为 [0,1,9,16,100] 

>示例 2：
>>输入：nums = [-7,-3,2,3,11]
输出：[4,9,9,49,121]

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

#### 209.长度最小的子数组
>给定一个含有 n 个正整数的数组和一个正整数 target 。
找出该数组中满足其总和大于等于 target 的长度最小的 
子数组
[numsl, numsl+1, ..., numsr-1, numsr] ，并返回其长度。如果不存在符合条件的子数组，返回 0 。

>示例 1：
>>输入：target = 7, nums = [2,3,1,2,4,3]
输出：2
解释：子数组 [4,3] 是该条件下的长度最小的子数组。 

>示例 2：
>>输入：target = 4, nums = [1,4,4]
输出：1 

>示例 3：
>>输入：target = 11, nums = [1,1,1,1,1,1,1,1]
输出：0

```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        //1.暴力循环
        // int result = nums.length + 1;
        // int sum = 0;
        // int minArrLen = 0;
        // for(int i = 0; i < nums.length; i++){
        //     sum = 0;
        //     for(int j = i; j < nums.length; j++){
        //         sum = sum + nums[j];
        //         if(sum >= target){
        //             minArrLen = j - i + 1;
        //             result = result < minArrLen ? result : minArrLen;
        //             break;
        //         }
        //     }
        // }
        // return result == nums.length + 1 ? 0 : result;


        //2.滑动窗口(双指针)
        int star = 0;
        int result = nums.length + 1;
        int sum = 0;
        for(int end = 0; end < nums.length; end++){
            sum += nums[end];
            while(sum >= target){
                result = Math.min(result, end - star + 1);//防止新的比老的大取他们最小值 (end - star + 1):新字串的长度
                sum -= nums[star];//因为star指针要后移,所以字串就不应该包括它自己了
                star++;
            }
        }
        //如果返回值没变,则证明数组总和都不大于target,则没有字串返回0
        return result == nums.length + 1 ? 0 : result;
        /*
        定义两个指针,一个指向返回子串的初始位置,一个终止位置,定义一个返回值(初始化为数组数组总长+1 用来刷新和最后判断)
        初始化两个指针都指向0索引,然后移动终止指针开始寻找字串,直到找到和大于target的字串停止,然后起始指针后移并将那个位置的数从
        字串和中减去,往复循环
        */


        
    }
}
```

#### 59.螺旋矩阵||
>给你一个正整数 n ，生成一个包含 1 到 n2 所有元素，且元素按顺时针顺序螺旋排列的 n x n 正方形矩阵 matrix 。

>示例:
1 2 3
6 7 4
9 8 5
>>输入：n = 3
输出：[ [1,2,3],[8,9,4],[7,6,5] ]
示例 2：
输入：n = 1
输出：[ [1] ]

```java
class Solution {
    public static int[][] generateMatrix(int n) {
        int[][] result = new int[n][n];

        int up = 0;
        int down = n - 1;
        int left = 0;
        int right = n - 1;
        int num = 1;//填入的数字(初始为1)

        while(num <= n*n){
            //1.如果n=1 数组就一个元素,则填入1,直接退出循环
            if(n == 1) {
                result[0][0] = 1; 
                break;
            }

            //2.n != 1时循环成立
            //从左到右
            for(int i = left; i <= right; i++){
                result[up][i] = num++;
            }
            up++;//上界下移

            //从上到下
            for(int i = up; i <= down; i++){
                result[i][right] = num++;
            }
            right--;//右界左移


            //从右到左
            if(up <= down){
                for(int i = right; i >= left; i--){
                    result[down][i] = num++;
                }
                down--;//下届上移
            }


            //从下到上
            if(left <= right){
                for(int i = down; i >= up; i--){
                    result[i][left] = num++;
                }
                left++;//左界右移
            }


        }

        return result;
    }
}

```

#### 203. 移除链表元素

给你一个链表的头节点 head 和一个整数 val ，请你删除链表中所有满足 Node.val == val 的节点，并返回 新的头节点 。
 

>示例 1：
>>输入：head = [1,2,6,3,4,5,6], val = 6
输出：[1,2,3,4,5] 

>示例 2：
>>输入：head = [], val = 1
输出：[] 

>示例 3：
>>输入：head = [7,7,7,7], val = 7
输出：[]

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution 
{
    public ListNode removeElements(ListNode head, int val) 
    {
        // 删除头节点值等于val的节点
        while (head != null && head.val == val){
            head = head.next; // 更新头节点
        }

        // 遍历链表，找到所有值为val的节点并删除
        ListNode temp = head;
        while (temp != null && temp.next != null){
            if (temp.next.val == val){
                temp.next = temp.next.next;//删除操作(前结点的指针,指向他的下下个结点)
            } else {
                temp = temp.next;//指针后移
            }
        }

        return head;
        
        /*
        头结点的值为val的问题:
            如:[1,1,1,1]  val = 1
            循环遍历找到头结点不为val的结点,把它定为头结点

        中间结点的值为val的问题:
            定义一个临时结点指向头结点
            (如果临时结点执向head.next 如果head.next的值为val
            则无法删除该结点,因为需要前一个结点的指针指向删除结点的后一个结点)
            找到该结点则执行删除该结点操作
            然后指针后移

        */
    }
}
``` 

### 

```java

```
