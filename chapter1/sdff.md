# Longest Substring Without Repeating Characters

---

Given a string, find the length of the longest substring without repeating characters.

Example：
 - Given "abcabcbb", the answer is "abc", which the length is 3.
 - Given "bbbbb", the answer is "b", with the length of 1.
 - Given "", the answer is "", with the length of 0.
 
 输出的是长度，也就是length value
 
 ## 思路
 
 遍历字符串每个字符，并且把字符和其位置存入一个map/dict,在遍历新的字符的时候
 - 判断这个字符在map里有没有出现
 - 判断目前map的长度是不是最长的
 所以我们需要
  + 一个遍历的标记：start 去存储搜寻substring的起始位置
  + 一个temporary dictionary存储用过的字母 usedChar = {}
  + 一个记录存储当前最长length的变量 maxLength
  
  ```py
  class Solution:
    # @return an integer
    def lengthOfLongestSubstring(self, s):
        start = maxLength = 0
        usedChar = {}
        
        for i in range(len(s)):
            if s[i] in usedChar and start <= usedChar[s[i]]:
                start = usedChar[s[i]] + 1
            else:
                maxLength = max(maxLength, i - start + 1)

            usedChar[s[i]] = i

        return maxLength

    if __name__ == "__main__":
        assert Solution().lengthOfLongestSubstring("abceads") == 6
  ```
 