---
title: "Insert Into Binary Search Tree [701]"
date: 2023-03-20T08:00:57+01:00
draft: false
summary: "You are given the root node of a binary search tree (BST) and a value to insert into the tree. Return the root node of the BST after the insertion. It is guaranteed that the new value does not exist in the original BST."
tags:
  - "leetcode"
  - "medium"
  - "bst"
  - "day10"
images:
  - "solution.png"
---

## Problem

You are given the `root` node of a binary search tree (BST) and a value to insert into the tree. Return the root node of the BST after the insertion. It is __guaranteed__ that the new value does not exist in the original BST.

## Solution

```dart {linenos=inline}
class Solution {
  TreeNode? insertIntoBST(TreeNode? root, int val) {
    TreeNode? node = root;
    while (node != null) {
      if (val > node!.val) {
        if (node.right != null) node = node.right;
        else {
          node.right = TreeNode(val);
          return root;
        }
      } else {
        if (node.left != null) node = node.left;
        else {
          node.left = TreeNode(val);
          return root;
        }
      }
    }
    return TreeNode(val);
  }
}
```
