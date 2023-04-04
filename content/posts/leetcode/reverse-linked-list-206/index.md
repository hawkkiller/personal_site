---
title: "Reverse Linked List 206"
date: 2023-04-04T07:24:44+02:00
draft: false
summary: "Given the `head` of a singly linked list, reverse the list, and return the reversed list."
featuredImage: "preview.png"
images:
  - "leetcode24.png"
tags:
  - "LeetCode"
  - "Iterative"
  - "Easy"
  - "linked list"
  - "day24"
---

## Problem

Given the `head` of a singly linked list, reverse the list, and return the reversed list.

<https://leetcode.com/problems/reverse-linked-list/>

### Example 1

Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]

### Example 2

Input: head = [1,2]
Output: [2,1]

### Example 3

Input: head = []
Output: []

## Solution

```dart {linenos=inline}
class Solution {
  ListNode? reverseList(ListNode? head) {
    ListNode? previous;
    ListNode? curr = head;

    while (curr != null) {
      final temp = curr?.next;
      curr?.next = previous;
      previous = curr;
      curr = temp;
    }
    return previous;
  }
}
```

## Complexity

Time complexity: O(n)

Space complexity: O(1)

## Explanation

The method works by creating two variables called previous and curr, which are initially null and set to the head of the list, respectively. The method then enters a while loop, which continues as long as curr is not null.

Inside the loop, the code creates a temporary variable called temp, which stores a reference to the next node in the list. The code then sets the next pointer of the current node (curr) to point to the previous node (previous), effectively reversing the order of the list up to that point. The code then updates the previous and curr variables to move to the next nodes in the list.

Finally, the method returns the new head of the reversed list, which is the last node that was assigned to the previous variable.
