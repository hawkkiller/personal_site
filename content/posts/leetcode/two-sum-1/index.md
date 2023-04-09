---
title: "Two Sum 1"
date: 2023-04-08T10:19:26+02:00
draft: false
summary: "Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target."
featuredImage: "preview.png"
images:
  - "preview.png"
tags:
  - "leetcode"
  - "easy"
  - "hashmap"
---

## Problem

Given an array of integers `nums` and an integer `target`, return *indices of the two numbers such that they add up to `target`*.

You may assume that each input would have **exactly one solution**, and you may not use the same element twice.

You can return the answer in any order.

### Example 1

Input: nums = [2,7,11,15], target = 9

Output: [0,1]

Output: Because nums[0] + nums[1] == 9, we return [0, 1].

### Example 2

Input: nums = [3,2,4], target = 6

Output: [1,2]

### Example 3

Input: nums = [3,3], target = 6

Output: [0,1]

## Solution

```dart
  List<int> twoSum(List<int> nums, int target) {
    final ht = <int, int>{};

    for (int i = 0; i < nums.length; i++) {
      if (ht[nums[i]] != null) {
        return [ht[nums[i]]!, i];
      }
      ht[target - nums[i]] = i;
    }
    return [-1,-1];
  } 
```

## Explanation

We use a hash table to store the difference between the target and the current number. If the current number is in the hash table, we return the index of the current number and the index of the number in the hash table. Otherwise, we add the difference to the hash table.

## Complexity

Time complexity: O(n)

Space complexity: O(n)
