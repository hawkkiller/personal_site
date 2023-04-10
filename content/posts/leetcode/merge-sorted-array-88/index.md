---
title: "Merge Sorted Array 88"
date: 2023-04-10T08:45:46+02:00
draft: false
summary: "Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array."
featuredImage: "preview.png"
images:
  - "preview.png"
tags:
  - "leetcode"
  - "easy"
  - "dart"
---

## Problem

Given two sorted integer arrays `nums1` and `nums2`, merge `nums2` into `nums1` as one sorted array.

The number of elements initialized in `nums1` and `nums2` are `m` and `n` respectively. You may assume that `nums1` has a size equal to `m + n` such that it has enough space to hold additional elements from `nums2`.

## Example

```dart
Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
Output: [1,2,2,3,5,6]
```

## Solution

```dart
  void merge(List<int> nums1, int m, List<int> nums2, int n) {
    int num1 = m - 1;
    int num2 = n - 1;

    for (int i = m + n - 1; i >= 0; i--) {
      if (num2 < 0) break;
      if (num1 >= 0 && nums1[num1] > nums2[num2]) {
        nums1[i] = nums1[num1--];
      } else {
        nums1[i] = nums2[num2--];
      }
    }
  }
```

## Explanation

Imagine you have two piles of cards, one with "m" cards and another with "n" cards. Each card has a number written on it. The cards in each pile are already sorted, but you want to merge them into one big pile while keeping the numbers in order.

To do this, you can start by placing the largest cards from each pile on top of each other in the big pile. Since the two piles are sorted, you know that the largest card in each pile is at the end of the pile. So, you start by comparing the last card in each pile (i.e. nums1[m-1] and nums2[n-1]) and placing the larger one at the end of the big pile (i.e. nums1[m+n-1]).

Then, you move on to the second largest cards from each pile and repeat the process, placing the larger one next in the big pile. You keep doing this until you've placed all the cards from both piles in the big pile.

However, there's a catch! Sometimes, one of the piles might run out of cards before you've finished merging them. In that case, you can just take the remaining cards from the other pile and place them in the big pile, because you know they're already sorted.

In the code, the algorithm is implemented using two indices, "num1" and "num2", that start at the end of each list and move towards the beginning. The loop iterates over the indices of the big pile, starting from the end and moving towards the beginning. At each iteration, it compares the values of the cards at the current indices in the two piles and places the larger one in the current index of the big pile. The indices of the pile from which the larger card was taken are decremented. If one of the piles runs out of cards before the other, the loop breaks and the remaining cards from the other pile are simply copied to the big pile.
