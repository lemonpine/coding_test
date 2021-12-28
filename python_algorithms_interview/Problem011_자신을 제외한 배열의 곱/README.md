# Problem 자신을 제외한 배열의 곱

https://leetcode.com/problems/product-of-array-except-self/



- #### Problem : 입력 받은 숫자들에 대해 각 숫자가 자신을 제외한 다른 값들의 곱을 Return 하되 '/' 나누기를 사용하지 않고 풀기

  

  Example 1:

    ```
  Input: nums = [1,2,3,4]
  Output: [24,12,8,6]
    ```

  Example 2:

    ```
  Input: nums = [-1,1,0,-3,3]
  Output: [0,0,9,0,0]
    ```

  ----------------------------------------------------

  

- #### Solution 1

  ```python
  # 1548 ms	40.5 MB	python3
  # Runtime: 1548 ms, faster than 5.05% of Python3 online submissions for Product of Array Except Self.
  # Memory Usage: 40.5 MB, less than 7.90% of Python3 online submissions for Product of Array Except Self.
  import numpy as np
  from typing import List
  class Solution:
      def productExceptSelf(self, nums: List[int]) -> List[int]:
          result = np.ones(len(nums), dtype = np.int16)
          for n, val in enumerate(nums):
              result[:n] *= val
              result[n+1:] *= val
          
          return list(result)
  ```
  
  Numpy Library 함수를 사용하여 선택된 인덱스를 제외한 왼쪽, 오른쪽의 인덱스 값에 선택된 값을 곱하는 방식
  
  *기본 Library가 아닌 다른 라이브러리 참조를 주의해야 하며, 또한 성능도 좋지 못함
  
  ​    
  
- #### Solution 2

  ```python
  # 232 ms	21.2 MB	python3
  # Runtime: 232 ms, faster than 83.89% of Python3 online submissions for Product of Array Except Self.
  # Memory Usage: 21.2 MB, less than 59.22% of Python3 online submissions for Product of Array Except Self.
  from typing import List
  class Solution:
      def productExceptSelf(self, nums: List[int]) -> List[int]:
          result = []
          # left product
          p = 1
          for i in range(len(nums)):
              result.append(p)
              p *= nums[i]
  
          # right product
          p = 1
          for i in range(len(nums) - 1, -1 , -1):
              result[i] = result[i] * p
              p *= nums[i]
          
          return result
  ```
  
  각 인덱스의 좌측부터의 누적 곱, 우측부터의 누적곱을 각각 저장한 후 최종적으로 곱하는 방식의 O(n) 풀이 방식
  
  
  
- #### Point

  