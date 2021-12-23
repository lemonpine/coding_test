# Problem 세수의 합

https://leetcode.com/problems/3sum



- #### Problem : 배열을 입력 받아 합을 0으로 만드는 3개의 엘리멘트를 출력

  

  Example 1:

    ```
  Input: nums = [-1,0,1,2,-1,-4]
  Output: [[-1,-1,2],[-1,0,1]]
    ```

  Example 2:

    ```
  Input: nums = []
  Output: []
    ```

  Example 3:

    ```
  Input: nums = [0]
  Output: []
    ```

  ----------------------------------------------------

  

- #### Solution 1

  ```python
  # 820 ms	17.6 MB	python3
  # Runtime: 820 ms, faster than 77.15% of Python3 online submissions for 3Sum.
  # Memory Usage: 17.6 MB, less than 50.17% of Python3 online submissions for 3Sum.
  
  from typing import List
  class Solution:
      def threeSum(self, nums: List[int]) -> List[List[int]]:
          
          result = []
          nums.sort()
          for f_i, first in enumerate(nums[:-2]):
              
              if f_i > 0 and nums[f_i] == nums[f_i-1]:
                  continue
              
              s_i, t_i = f_i + 1, len(nums) - 1
              while s_i < t_i:
                  three_sum = first + nums[s_i] + nums[t_i]
                  if three_sum == 0:
                      result.append([first, nums[s_i], nums[t_i]])
                      while s_i < t_i and nums[s_i] == nums[s_i+1]:
                          s_i += 1
                      while s_i < t_i and nums[t_i] == nums[t_i-1]:
                          t_i -= 1                    
                      s_i += 1
                      t_i -= 1
                  elif three_sum < 0:
                      s_i += 1
                  else:
                      t_i -= 1
          
          return result
  ```
  
  Two Pointer를 활용하며, Pointer가 이동함에 따라 중복이 있으면 한칸더 이동하는 방식으로 계산
  
  ​    

- #### Point

  문제를 단순화하여 Two Pointer로 처리 