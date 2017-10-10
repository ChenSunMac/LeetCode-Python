# Longest Palindromic Substring

Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

palindromic是回文的意思

Example：
 - Input: "babad"
  - Output: "bab" or "aba"
  
 - Input:"cbbbbd"
  - Output: "bbbb"
  
## 思路

  **这里的难点是区分palindro的两种情况，一种是奇数，一种是偶数**。
  那么我们需要遍历字符串每个字符，
  - 如果这是第偶数个（其编号为奇数），则利用left 和 right 去继续搜索回文
  - vice versa，left 和 right的编号会相差1
  - 那么 在持续满足 s[left] == s[right] 时， 继续增长left 和 right
  并且在跳出循环 （即 不满足回文条件时）
  - 比较当前最大的longest （利用**maxDistance**去记录）
  - 记录回文的开头和结尾 _begin and end_
  
  