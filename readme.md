# Leetcode-Python-2024
Solution for All Leetcode DSA practice questions for 2024.

Zero to Hero in Leetcode DSA in 2024.

## [169. Majority Element](https://leetcode.com/problems/majority-element/description/?envType=daily-question&envId=2024-02-12)
```python
### Return the majority element in a list
"""
Input: nums = [3,2,3]
Output: 3
"""
class Solution:
    def majorityElement(self, nums:List[int])->int:
        # O(n); Use hash table with frequency as value
        counter_arr = {}
        for element in nums:
            if element in counter_arr:
                counter_arr[element]+=1
            else:
                counter_arr[element]=1
        return max(counter_arr, key=counter_arr.get)
```
#### Best Solution using O(n) time and O(1) space
```python
# Boyer-Moore Majority Vote Algorithm
# This algorithm works on the fact that if an element occurs more than N/2 times, it means that
# the remaining elements other than this would definitely be less than N/2
class Solution:
    def majorityElement(self, nums:List[int])->int:
        candidate=None
        count=0
        for element in nums:
            if candidate is None or count==0:
                candidate=element
                count+=1
            elif element==candidate:
                count+=1
            else:
                count-=1
        return candidate
```

## [26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)
```python
"""
Remove duplicates from a sorted array and return the number of unique elements.
"""
# Noob solution Use set and [:] for inplace operaion in python
class Solution:
    def removeDuplicates(self, nums:List[int])->int:
        nums[:] = sorted(set(nums))
        return len(nums)
```
### Best Solution O(N)time and O(1) space
```python
# Two Pointer solution
class Solution:
    def removeDuplicates(self, nums:List[int])->int:
        # Check for empty lists
        if len(nums)==0:
            return 0
        unique = i= 1
        for i in range(1,len(nums)):
            if nums[i] != nums[i-1]:
                # Use unique as key for unique index
                nums[unique] = nums[i]
                unique+=1
        return unique
```
## [2108. Find First Palindromic String in the Array](https://leetcode.com/problems/find-first-palindromic-string-in-the-array/description/?envType=daily-question&envId=2024-02-13)
```python
"""
Return the first palindrome in the list of strings.
"""
# Noob's Solution
# Time Complexity = O(n.m); n is the no. of words and m is the length of words
# Space complexity =
class Solution:
    def firstPalindrome(self, words:List[str])->str:
        for word in words:
            if word[:] == word[::-1]:
                # Return First Palindrome
                return word
        ## Palindrome not found return empty string
        return ""
```
### Solution Using Two Pointers
```python
# Two Pointer Solution
# Time Complexity = O(n.m); n is the no. of words and m is the length of words
# Space complexity = O(1)
class Solution:
    def check_palindrome(self,word:str)->bool:
        i,j = 0,len(word)-1
        while(i<=j):
            if word[i] == word[j]:
                i+=1
                j-=1
            else:
                return False
        return True
    def firstPalindrome(self, words:List[str])->str:
        for word in words:
            if self.check_palindrome(word):
                return word
        ## Palindrome not found return empty string
        return ""
```
## [1. Two Sum](https://leetcode.com/problems/two-sum/description/)
```python
class Solution:
    def twoSum(self,nums:List[int],target:int)->List[int]:
        # Brute Force Slution O(n^2)
        for i in range(0, len(nums)-1):
            for j in range(i+1, len(nums)):
                if nums[i]+nums[j]==target:
                    return [i, j]
        return ""
```
#### Optimal Solution using Dictionary/Hashmap. O(n) time complexity and O(n) space complexity
```python
# Using hashmap
class Solution:
    def twoSum(self, nums:List[int], target:int)->List[int]:
        # Create empty hashmap
        hash_map={}
        for i in range(0,len(nums)):
            if nums[i] in hash_map:
                return [i, hash_map[nums[i]]]
            else:
                hash_map[target - nums[i]]=i
        return []
```

## [35. Search Insert Position](https://leetcode.com/problems/search-insert-position/description/)
```python
"""
Sorted array of integers
Search for the target in the sorted array in O(log n)
If not found retrun its possible index
"""
# Using Binary Search Logic
# Time Complexity : O(log n)
# Space Compleity : O(1)
class Solution:
    def searchInsert(self, nums:List[int],target:int)->int:
        low,high=0,len(nums)-1
        while(low<=high):
            mid = (low+high)//2
            if nums[mid]==target:
                return mid
            elif nums[mid]>target:
                high=mid-1
            else:
                low=mid+1
        # Return nearest index for target if not in nums
        if target<nums[mid]:
            return mid
        else:
            return mid+1
```

# Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.


# License
[MIT](https://choosealicense.com/licenses/mit/)
