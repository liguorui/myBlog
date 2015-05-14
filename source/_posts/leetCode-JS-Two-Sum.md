title: "leetCode[JS] - Two Sum"
date: 2015-05-14 10:28:38
tags: "leetCode"
---
## Two Sum

Difficulty : [Medium] -- [访问链接](https://leetcode.com/problems/two-sum/)

### 题目

{% blockquote %}
Given an array of integers, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.

You may assume that each input would have exactly one solution.

Input: numbers={2, 7, 11, 15}, target=9
Output: index1=1, index2=2
{% endblockquote %}

### 简要翻译

{% blockquote %}
问题描述：在一个数组（无序）中快速找出两个数字，使得两个数字之和等于一个给定的值。
输入：一个整型数组numbers 和 一个同为整型的目标值target
输出：为数组，如果找到则返回长度为二的数组，index1的值小于index2的值，未找到则返回空数组
{% endblockquote %}

### 分析

{% blockquote %}
如何从数组中找到两个数之和等于目标值。
首先想到的就是暴力查找，每个数和其他数进行相加，判断和是否等于目标值，这必然是不满足该题出题者的想法的。
如何进行查找优化，如果进行每一次查找，我们可以更加接近目标值则满足该要求。
{% endblockquote %}

### 提交代码
{% codeblock %}
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
  var len = nums.length, r =[], i = 0, j = 1, sortA = nums.concat().sort(function(a, b){return a - b})
  for(;i + j < len;){
    var x = sortA[i], y = sortA[len - j]
    if(x + y == target){
      r = [nums.indexOf(x)+1, nums.lastIndexOf(y) + 1]
      return r[0] < r[1] ? r : [r[1], r[0]]
    }
    else if(x + y < target) i++
    else j++
  }
  return r
};
{% endcodeblock %}

### 代码剖析

1. 查找数组是升序或者降序排列。（对数据进行排序，同时要保留原有数组，则拷贝排序）
{% blockquote %}
使用concat对数组进行拷贝 [javascript 三种数组复制方法的性能对比](http://www.jb51.net/article/21918.htm)，大家有兴趣可以去对比一下数组拷贝的性能。然后使用sort进行升序排列
{% codeblock %}
nums.concat().sort(function(a, b){return a - b})
{% endcodeblock %}
{% endblockquote %}

2. 有规律的移动两个数。（以开始和末尾的两个数字开始，两数之和大于目标值target，则需要一个较小的因子，末尾端的数字向前移动；反之，开始端的数字向后移动。直至找到最终的结果）
{% blockquote %}
用i + j < len来保证只遍历一遍数组
{% codeblock %}
for(;i + j < len;){
  var x = sortA[i], y = sortA[len - j]
  if(x + y == target){
    // x 和 y 为找到的结果数
  }
  else if(x + y < target) i++
  else j++
}
{% endcodeblock %}
{% endblockquote %}

3. 获取两值在原有数组的索引。（将找到的两个结果数在原有数组中找到其位置，并按照升序排列）
{% blockquote %}
查找y所在位置的时候使用了lastIndexOf，这是为了解决如果x==y，而y需要获取到后面一个数的索引
{% codeblock %}
r = [nums.indexOf(x)+1, nums.lastIndexOf(y) + 1]
return r[0] < r[1] ? r : [r[1], r[0]]
{% endcodeblock %}
{% endblockquote %}

### 通过截图
{% img leetCode /images/leetCode001.png 100% leetCode001 %}
