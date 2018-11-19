---
title: LeetCode-1-TwoSum
date: 2018-11-19 16:28:26
tags: leetcode
---

#### Problem

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

### Example

```
Given nums = [2, 7, 11, 15], target = 9,
Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

### Solution
```
const TwoSum = (list, target) => {
  let hash = {};
  let len = list.length;

  for(let j = 0; j < list.length; j++) {
    if (list[j] in hash) {
      return [hash[list[j]], j];
    }
    hash[target - list[j]] = j;
  }
  return [-1, -1];
}
```
