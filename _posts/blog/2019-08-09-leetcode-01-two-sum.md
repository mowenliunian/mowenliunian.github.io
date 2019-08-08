---
layout: post
title: Two Sum
categories: [algorithm, leetcode]
description: 找出数组中加和等于某个值得两个整数位置。
keywords: algorithm, leetcode, two sum
---

> Given an array of integers, return indices of the two numbers such that they add up to a specific target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.
([leetcode](https://leetcode.com/problems/two-sum/))


## Example

> Given nums = [2, 7, 11, 15], target = 9,  
Because nums[0] + nums[1] = 2 + 7 = 9,  
return [0, 1].


## Solutions

### S1：暴力求解（Brute Force）

> 循环遍历每个元素 x，并对于每个 x 遍历其余元素 y，直到找到满足 x + y = target 的 x 和 y 为止。
由于需要进行两层循环遍历，时间复杂度为 O(n<sup>2</sup>)。不需要其它额外的存储空间，空间复杂度为 O(1)。

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

### S2：利用HashMap

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