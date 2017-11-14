# Missing Number
---
Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the one that is missing from the array.

For example,
Given nums = [0, 1, 3] return 2

---
最brutal force应该就是直接sort， 然后再从头loop到和序号number不一样的那个位置就行了
Time complexity : O(nlogn)
Space complexity : O(n)

---
为了降低时间复杂度，我们可以通过map/dict/set去做：
```py
def missingNumber(nums):
    num_set = set(nums)
    n = len(nums) + 1
    for number in range(n):
        if number not in num_set:
            return number
```
Time complexity : O(n)(Because the set allows for O(1) containment queries and Creating num_set costs O(n) time)

---