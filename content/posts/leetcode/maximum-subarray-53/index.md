---
title: "Maximum Subarray 53"
date: 2023-04-07T09:47:05+02:00
draft: false
summary: "Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum."
resources:
  - name: "featured-image"
    src: "preview.png"
tags:
  - "day25"
  - "leetcode"
  - "medium"
  - "array"
  - "dynamic programming"
---

## Problem

Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

<https://leetcode.com/problems/maximum-subarray/>

### Example 1

Input: nums = [-2,1,-3,4,-1,2,1,-5,4]

Output: 6

Explanation: [4,-1,2,1] has the largest sum = 6.

### Example 2

Input: nums = [1]

Output: 1

### Example 3

Input: nums = [5,4,-1,7,8]

Output: 23

## Solution

```dart {linenos=inline}
  int maxSubArray(List<int> nums) {
    if (nums.isEmpty) return 0;
    
    int maxSum = nums[0];
    int curSum = nums[0];

    for (int i = 1; i < nums.length; i++) {
      curSum = max(nums[i], curSum + nums[i]);
      maxSum = max(curSum, maxSum);
    }

    return maxSum;
  }
```

## Explanation

The solution is based on the [Kadane's algorithm](https://en.wikipedia.org/wiki/Maximum_subarray_problem#Kadane's_algorithm). The algorithm is based on the idea that the maximum subarray sum ending at the current position is either the current element or the current element plus the maximum subarray sum ending at the previous position. The maximum subarray sum ending at the previous position is stored in the `curSum` variable. The maximum subarray sum is stored in the `maxSum` variable.

## Complexity

Time complexity: O(n)

Space complexity: O(1)
