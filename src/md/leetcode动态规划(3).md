1.
198.打家劫舍
你是一个专业的小偷，计划偷窃沿街的房屋。每间房内都藏有一定的现金，影响你偷窃的唯一制约因素就是相邻的房屋装有相互连通的防盗系统，如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警。

给定一个代表每个房屋存放金额的非负整数数组，计算你 不触动警报装置的情况下 ，一夜之内能够偷窃到的最高金额。



示例 1：

输入：[1,2,3,1]
输出：4
解释：偷窃 1 号房屋 (金额 = 1) ，然后偷窃 3 号房屋 (金额 = 3)。
     偷窃到的最高金额 = 1 + 3 = 4 。
示例 2：

输入：[2,7,9,3,1]
输出：12
解释：偷窃 1 号房屋 (金额 = 2), 偷窃 3 号房屋 (金额 = 9)，接着偷窃 5 号房屋 (金额 = 1)。
     偷窃到的最高金额 = 2 + 9 + 1 = 12 。

**代码:**
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
//var rob = function (nums) {
// 有bug不会写
//   let count = 0;
//   for (let i = 0; i < nums.length; i++) {
//     count = Math.max(count, money(i));
//   }

//   function money(index) {
//     let count = 0;
//     for (let m = index; m < nums.length; m += 2) {
//       count += nums[m];
//     }
//     for (let j = index; j > 0; j -= 2) {
//       if (j == index) continue;
//       count += nums[j];
//     }
//     return count;
//   }

//   return count;
// };

var rob = function(nums) {
    const len = nums.length;
    if(len == 0)
        return 0;
    const dp = new Array(len + 1);

    dp[0] = 0;
    dp[1] = nums[0];
    for(let i = 2; i <= len; i++) {
        dp[i] = Math.max(dp[i-1], dp[i-2] + nums[i-1]);
    }
    return dp[len];
};
```
2.
213.打家劫舍 II
你是一个专业的小偷，计划偷窃沿街的房屋，每间房内都藏有一定的现金。这个地方所有的房屋都 围成一圈 ，这意味着第一个房屋和最后一个房屋是紧挨着的。同时，相邻的房屋装有相互连通的防盗系统，如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警 。

给定一个代表每个房屋存放金额的非负整数数组，计算你 在不触动警报装置的情况下 ，今晚能够偷窃到的最高金额。



示例 1：

输入：nums = [2,3,2]
输出：3
解释：你不能先偷窃 1 号房屋（金额 = 2），然后偷窃 3 号房屋（金额 = 2）, 因为他们是相邻的。
示例 2：

输入：nums = [1,2,3,1]
输出：4
解释：你可以先偷窃 1 号房屋（金额 = 1），然后偷窃 3 号房屋（金额 = 3）。
     偷窃到的最高金额 = 1 + 3 = 4 。
示例 3：

输入：nums = [1,2,3]
输出：3

**代码:**
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var rob = function(nums) {
    // 官方题解 下面呢个函数没看太懂  下次再来
    const length = nums.length
    if(length === 1) {
        return nums[0]
    }else if(length === 2) {
        return Math.max(nums[0], nums[1])
    }
    return Math.max(robRange(nums, 0, length - 2), robRange(nums, 1, length - 1))

    function robRange(nums, start, end) {
        let  first = nums[start], second = Math.max(nums[start], nums[start + 1])
        for(let i = start + 2; i <= end; i++) {
            const temp = second
            second = Math.max(first + nums[i], second)
            first = temp
        }
        return second
    }
};
```
3.
740.删除并获得点数
给你一个整数数组 nums ，你可以对它进行一些操作。

每次操作中，选择任意一个 nums[i] ，删除它并获得 nums[i] 的点数。之后，你必须删除 所有 等于 nums[i] - 1 和 nums[i] + 1 的元素。

开始你拥有 0 个点数。返回你能通过这些操作获得的最大点数。



示例 1：

输入：nums = [3,4,2]
输出：6
解释：
删除 4 获得 4 个点数，因此 3 也被删除。
之后，删除 2 获得 2 个点数。总共获得 6 个点数。
示例 2：

输入：nums = [2,2,3,3,3,4]
输出：9
解释：
删除 3 获得 3 个点数，接着要删除两个 2 和 4 。
之后，再次删除 3 获得 3 个点数，再次删除 3 获得 3 个点数。
总共获得 9 个点数。


**代码:**
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var deleteAndEarn = function(nums) {
    // 完全不会哎!
};
```