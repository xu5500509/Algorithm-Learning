---
layout:     post
title:      LintCode公开比赛-Career Fair Warm Up I
category: blog
description: 题目：平面列表，骰子求和，将数组重新排序以构造最小值，克隆二叉树
---

## 1. 平面列表

给定一个列表，该列表中的每个要素要么是个列表，要么是整数。将其变成一个只包含整数的简单列表。

### 样例
给定 [1,2,[1,2]]，返回 [1,2,1,2]。
给定 [4,[3,[2,[1]]]]，返回 [4,3,2,1]。

### 挑战
请用非递归方法尝试解答这道题。


### 答案
    /**
     * // This is the interface that allows for creating nested lists.
     * // You should not implement it, or speculate about its implementation
     * public interface NestedInteger {
     *
     *     // @return true if this NestedInteger holds a single integer,
     *     // rather than a nested list.
     *     public boolean isInteger();
     *
     *     // @return the single integer that this NestedInteger holds,
     *     // if it holds a single integer
     *     // Return null if this NestedInteger holds a nested list
     *     public Integer getInteger();
     *
     *     // @return the nested list that this NestedInteger holds,
     *     // if it holds a nested list
     *     // Return null if this NestedInteger holds a single integer
     *     public List<NestedInteger> getList();
     * }
     */
    public class Solution {
    
        // @param nestedList a list of NestedInteger
        // @return a list of integer
        public List<Integer> flatten(List<NestedInteger> nestedList) {
            // Write your code here
            List<Integer> result = new ArrayList<Integer>();
            for (NestedInteger ele : nestedList)
                if (ele.isInteger())
                    result.add(ele.getInteger());
                else
                    result.addAll(flatten(ele.getList()));
            return result;
        }
    }
    
    //non-recursive version
    public class Solution {
    
        // @param nestedList a list of NestedInteger
        // @return a list of integer
        public List<Integer> flatten(List<NestedInteger> nestedList) {
            boolean isFlat = true;
            while (isFlat) {
                isFlat = false;
                List<NestedInteger> newLs = new ArrayList<>();
                for (NestedInteger ni : nestedList) {
                    if (ni.isInteger()) {
                        newLs.add(ni);
                    } else {
                        newLs.addAll(ni.getList());
                        isFlat = true;
                    }
                }
                nestedList = newLs;
            }
            List<Integer> r = new ArrayList<>();
            for (NestedInteger ni : nestedList) {
                r.add(ni.getInteger());
            }
            return r;
        }
    }

### 个人总结

上面有两种写法，第一种为递归，第二种非递归。
递归的写法，很容易就想出来了。第二种就是用一个while循环取代递归。
for循环都可以用while表示，但是while循环不一定可以用for，第二种while的写法就是一个例子了，不能用for替代。