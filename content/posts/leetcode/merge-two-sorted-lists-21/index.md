---
title: "Merge Two Sorted Lists [21]"
date: 2023-04-03T19:01:08+02:00
draft: false
summary: "You are given the heads of two sorted linked lists list1 and list2. Merge the two lists in a one sorted list. The list should be made by splicing together the nodes of the first two lists."
featuredImage: "preview.png"
images:
  - "leetcode23.png"
tags:
  - "leetcode"
  - "iterative"
  - "medium"
  - "linked list"
  - "day23"
---

## Problem

You are given the heads of two sorted linked lists list1 and list2.

Merge the two lists in a one sorted list. The list should be made by splicing together the nodes of the first two lists.

Return the head of the merged linked list.

<https://leetcode.com/problems/merge-two-sorted-lists/>

### Example 1

Input: list1 = [1,2,4], list2 = [1,3,4]
Output: [1,1,2,3,4,4]

### Example 2

Input: list1 = [], list2 = []
Output: []

### Example 3

Input: list1 = [], list2 = [0]
Output: [0]

## Solution

```dart {linenos=inline}
ListNode? mergeTwoLists(ListNode? list1, ListNode? list2) {
  if (list1 == null) return list2;
  if (list2 == null) return list1;

  final merged = ListNode();
  ListNode? prev = merged;

  while (list1 != null && list2 != null) {
    if (list1!.val <= list2!.val) {
      prev!.next = list1;
      list1 = list1?.next;
    } else {
      prev!.next = list2;
      list2 = list2?.next;
    }
    prev = prev!.next;
  }

  prev!.next = list1 == null ? list2 : list1;

  return merged.next;
}
```

## Complexity

Time: O(n + m)

Space: O(1)

## Explanation

This code defines a function called mergeTwoLists that takes two ListNode objects (list1 and list2) as input, and returns a new ListNode object that contains the merged values from both lists. The function first checks if either of the input lists is null, and returns the other list if that is the case.

Next, the function creates a new ListNode object called merged, and initializes a new variable prev to point to merged. Then, using a while loop, the function iterates through both lists and compares the values of the nodes at the current position. If the value in list1 is less than or equal to the value in list2, the node from list1 is added to the merged list, and list1 is moved to the next node. Otherwise, the node from list2 is added to the merged list, and list2 is moved to the next node. The prev variable is also updated to point to the current node in the merged list.

After the while loop is completed, the function adds any remaining nodes from either list1 or list2 to the merged list, depending on which list still has nodes remaining. Finally, the function returns the merged list.

Overall, this function is used to merge two sorted lists into a new sorted list. It works by comparing the values of the nodes in each list, and adding them to the merged list in order.
