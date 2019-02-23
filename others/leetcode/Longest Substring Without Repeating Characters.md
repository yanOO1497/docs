# 无重复字符的最长子串
## 题目
给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。

示例 1:
```
输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```
示例 2:
```
输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```
示例 3:
```
输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
 ```
解答：
```js
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function(s) {
    let temp = [];
    let result = 0;
    for (let i = 0; i < s.length; i ++) {
        const index = temp.indexOf(s[i]);
        temp.push(s[i]);
         index !== -1 && (temp.splice(0, index + 1));
        result = Math.max(result, temp.length)
    }
    return result;
};
```
时间复杂度： O(n)

思路：
循环遍历传入的字符串，用一个临时数组存储获取到的子串，用一个变量存储当前不重复子串的最大值。遍历的过程中，如果当前字符与临时数组里没有重复的，就将该字符存入临时数组，同时更新变量取两者的最大值；如果当前字符与临时数组有重复的，记录当前位置，临时数组需要把重复的位置之前的数据都扔掉，继续循环。这样变量里存储的一直是字串的最大值。

