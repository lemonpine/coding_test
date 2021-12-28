# Problem 배열파티션1

https://leetcode.com/problems/array-partition-i/



- #### Problem : 짝수개의 숫자로 된 리스트를 입력받아 숫자를 2개씩 묶은 후 둘 중 작은 숫자들의 합의 최대값을 구하시오

  

  Example 1:

    ```
  Input: nums = [1,4,3,2]
  Output: 4
   # Explanation: All possible pairings (ignoring the ordering of elements) are:
   # 1. (1, 4), (2, 3) -> min(1, 4) + min(2, 3) = 1 + 2 = 3
   # 2. (1, 3), (2, 4) -> min(1, 3) + min(2, 4) = 1 + 2 = 3
   # 3. (1, 2), (3, 4) -> min(1, 2) + min(3, 4) = 1 + 3 = 4
   # So the maximum possible sum is 4.
    ```

  Example 2:

    ```
  Input: nums = [6,2,6,5,1,2]
  Output: 9
   # Explanation: The optimal pairing is (2, 1), (2, 5), (6, 6). min(2, 1) + min(2, 5) + min(6, 6) = 1 + 2 + 6 = 9.
    ```

  ----------------------------------------------------

  

- #### Solution 1

  ```python
  # 264 ms	16.8 MB	python3
  # Runtime: 264 ms, faster than 71.05% of Python3 online submissions for Array Partition I.
  # Memory Usage: 16.8 MB, less than 32.63% of Python3 online submissions for Array Partition I.
  from typing import List
  class Solution:
      def arrayPairSum(self, nums: List[int]) -> int:
          nums.sort()
          result = 0
          for i in range(int(len(nums)/2)):
              result += nums[i*2]
          
          return result
  ```
  
  정렬 후 0, 2, 4 ... 짝수 인덱스를 같는 값 들의 합을 구함
  
  ​    
  
- #### Solution 2

  ```python
  # 248 ms	16.8 MB	python3
  # Runtime: 248 ms, faster than 97.85% of Python3 online submissions for Array Partition I.
  # Memory Usage: 16.8 MB, less than 32.63% of Python3 online submissions for Array Partition I.
  from typing import List
  class Solution:
      def arrayPairSum(self, nums: List[int]) -> int:
          nums.sort()
          return sum(nums[::2])
  ```
  
  for문이 아닌 python list slicing을 통해 바로 추출
  
  
  
- #### Point

  python에서 제공하는 간단한 함수들을 활용해보기