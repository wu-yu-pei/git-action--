#### [1. 乘积最大子数组](https://leetcode-cn.com/problems/maximum-product-subarray/)

难度中等

给你一个整数数组 `nums` ，请你找出数组中乘积最大的非空连续子数组（该子数组中至少包含一个数字），并返回该子数组所对应的乘积。

测试用例的答案是一个 **32-位** 整数。

**子数组** 是数组的连续子序列。

 

**示例 1:**

```
输入: nums = [2,3,-2,4]
输出: 6
解释: 子数组 [2,3] 有最大乘积 6。
```

**示例 2:**

```
输入: nums = [-2,0,-1]
输出: 0
解释: 结果不能为 2, 因为 [-2,-1] 不是子数组。
```

 **思路:**

+ 有点像动态规划,但是又不全像
+ 没解出来

**代码:**

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxProduct = function(nums) {
    // 没通过 少考虑了负负为正的情况  ac了50%
    // if(nums.length === 1) return nums[0]
    // let dp = [1, nums[0]]
    // for(let i = 2; i <= nums.length; i++) {
    //     dp[i] = Math.max(dp[i - 1]*nums[i-1], nums[i-1])
    // }
    // dp.splice(0,1)
    // console.log(dp)
    // return Math.max(...dp)

    // leetcode题解1: 没看懂
    // let curMax = nums[0];
    // let curMin = nums[0];
    // let res = nums[0];
    // for (let i = 1; i < nums.length; i++) {
    //     let temp1 = curMax * nums[i], temp2 = curMin * nums[i];
    //     curMax = Math.max(temp1, temp2, nums[i]);
    //     curMin = Math.min(temp1, temp2, nums[i]);
    //     res = Math.max(curMax, res);
    // }
    // return res;

  // 题解二 看懂了一部分
  let n = nums.length;
  let dp = new Array(n).fill(0).map(() => new Array(2).fill(0));
  /* base case */
  // 从第 0 项到第 i 项范围内的子数组的最小乘积
  dp[0][0] = nums[0];
  // 从第 0 项到第 i 项范围内的子数组的最大乘积
  dp[0][1] = nums[0];
  for (let i = 1; i < n; i++) {
    dp[i][0] = Math.min(
      // 不和别人乘就nums[i]自己
      nums[i],
      // nums[i]是负数，希望乘上前面的最小乘积
      dp[i - 1][0] * nums[i],
      // nums[i]是正数，希望乘上前面的最大乘积
      dp[i - 1][1] * nums[i]
    );
    dp[i][1] = Math.max(
      // 不和别人乘就nums[i]自己
      nums[i],
      // nums[i]是负数，希望乘上前面的最小乘积
      dp[i - 1][0] * nums[i],
      // nums[i]是正数，希望乘上前面的最大乘积
      dp[i - 1][1] * nums[i]
    );
  }
  return Math.max(...dp.map((item) => item[1]));
};    
```

下次一定(!__!)