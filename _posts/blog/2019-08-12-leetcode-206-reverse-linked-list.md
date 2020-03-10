---
layout: post
title: Reverse Linked List
categories: [algorithm, leetcode]
description: 反转单链表。
keywords: algorithm, leetcode, reverse linked list
---

> Reverse a singly linked list.
([leetcode](https://leetcode.com/problems/reverse-linked-list/))


## Example

>Input: 1->2->3->4->5->NULL  
 Output: 5->4->3->2->1->NULL


## Solutions

### S1：迭代

> 循环遍历每个节点，遍历过程中不断将当前节点指向前一个节点。由于当前节点不包含前一个节点的引用，
因此需要一个变量保存前一个节点。指向前一个节点前需要一个变量保存下一个节点，以便可以继续向下遍历。
需要遍历每个节点，时间复杂度为O(n)。反转过程中只需要3个节点变量，空间复杂度为O(1)。

```java
public int[] twoSum1(int[] nums, int target) {        
    int length = nums.length;
    for (int i = 0; i < length - 1; i++) {
        for (int j = i + 1; j < length; j++) {
            if (nums[i] + nums[j] == target) {
                return new int[]{i, j};
            }
        }
    }
    
    throw new RuntimeException("no solution");
}
```

### S2：递归

> 空间换时间。遍历每个元素的同时，利用 HashMap 记录遍历过的元素和下标。对于当前元素，
只需要检查 HashMap 是否已经存在符合条件的组合即可。单层遍历的时间复杂度为 O(n)，
HashMap 每次插入和查找的时间复杂度为 O(1)，总的时间复杂度为 O(n)。需要借助 HashMap 存储已经遍历的元素，
HashMap 最多会存储 n - 1 个元素，因此空间复杂度为 O(n)。

```java
public int[] twoSum2(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    int length = nums.length;
    for (int i = 0; i < length; i++) {
        if(map.containsKey(nums[i])){
            return new int[]{map.get(nums[i]), i};
        }

        map.put(target - nums[i], i);
    }
    
    throw new RuntimeException("no solution");
}
```