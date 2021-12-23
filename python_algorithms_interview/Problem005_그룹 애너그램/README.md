# Problem 그룹 애너그램

https://leetcode.com/problems/group-anagrams/



- #### Problem : 문자열을 받아 애너그램 단위로 그룹핑

  *문자열의 순서를 바꾸어 동일하다면 같은 애너그램 그룹으로 인식

  

  Example 1:
  
  ```
  Input: strs = ["eat","tea","tan","ate","nat","bat"]
  Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
```
  
Example 2:
  
  ```
  Input: strs = [""]
  Output: [[""]]
  ```

  Example 3:

  ```
  Input: strs = ["a"]
  Output: [["a"]]
  ```
  
  ---------------------

  

- #### Solution 1

  ```python
  # 96 ms	17.1 MB	python3
  # Runtime: 96 ms, faster than 81.63% of Python3 online submissions for Group Anagrams.
  # Memory Usage: 17.1 MB, less than 86.79% of Python3 online submissions for Group Anagrams.
  
  from typing import List
  class Solution:
      def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
          anagram_dict = {}
          for string_raw in sorted(strs):
              if "".join(sorted(string_raw)) in anagram_dict.keys():
                  anagram_dict["".join(sorted(string_raw))].append(string_raw)
              else: 
                  anagram_dict["".join(sorted(string_raw))] = [string_raw]
          return list(anagram_dict.values())
  ```

  같은 애너그램 그룹에 속하는지를 dictionary로 분류, 문자열의 정렬된 값을 Key값으로 하여

  애너그램 단위로 묶는 코드

  

- #### Point

  dictionary로 같은 key를 같는 value를 묶을 수 있으며,

  다양한 정렬 방법 (Quick sort, Merge sort 등 여러 정렬방법을 고민해볼 필요 있음)