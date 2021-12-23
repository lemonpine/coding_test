# Problem 빗물 트래핑

https://leetcode.com/problems/two-sum/



- #### Problem : 주어진 인풋으로 표현되는 아래와 같이 그림 사이에 물을 얼마나 쌓을수 있는지 계산

  ![문제그림](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)

  Example 1:

    ```
  Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
  Output: 6
   # Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. 
   # In this case, 6 units of rain water (blue section) are being trapped.
    ```

    Example 2:

    ```
  Input: height = [4,2,0,3,2,5]
  Output: 9
    ```

  ----------------------------------------------------

  

- #### Solution 1

  ```python
  # 3088 ms	15.7 MB	python3
  # Runtime: 3096 ms, faster than 5.04% of Python3 online submissions for Trapping Rain Water.
  # Memory Usage: 15.9 MB, less than 12.43% of Python3 online submissions for Trapping Rain Water.
  
  from typing import List
  class Solution:
      def trap(self, height: List[int]) -> int:
          
          water_sum = 0
          left, right = height.index(max(height)), height.index(max(height))
          
          def high_point_search(l_bound, r_bound):
              print(l_bound, '~', r_bound - 1)
              return l_bound + height[l_bound:r_bound].index(max(height[l_bound:r_bound]))
              
          def sub_water(l_high, r_high):
              minuses = 0
              for i in range(l_high + 1, r_high):
                  minuses += height[i]
              print('sub_water', min(height[l_high], height[r_high]) * (r_high - l_high - 1) - minuses)
              return min(height[l_high], height[r_high]) * (r_high - l_high - 1) - minuses
          
          
          # left search
          while right > 0:
              l_high_point = high_point_search(0, right)
              water_sum += sub_water(l_high_point, right)
              right = l_high_point
          
          # right search 
          # but, 가장 마지막 right를 찾도록 해야한다 
          while left < len(height) - 1:
              r_high_point = high_point_search(left + 1, len(height))
              water_sum += sub_water(left, r_high_point)
              left = r_high_point
          
          return water_sum
  ```

  각 봉우리를 찾고 그 안에 물이 얼마나 고일지 찾는 방법으로 

  시작은 가장 높은 값을 갖는 인덱스부터 좌우에 다음으로 큰 봉우리를 찾으며, 그 안에 채울 수 있는 물의 양을 계산

  많은 연산이 필요한 max index 계산 등이 포함되어있어, 전체 처리시간이 김

  

- #### Solution 2

  ```python
  # 1272 ms	32.6 MB	python3
  # Runtime: 1272 ms, faster than 5.01% of Python3 online submissions for Trapping Rain Water.
  # Memory Usage: 32.6 MB, less than 12.08% of Python3 online submissions for Trapping Rain Water.
      
  from typing import List
  import numpy as np
  class Solution:
      def trap(self, height: List[int]) -> int:
          result = 0
          
          npheight, high = np.array(height), 0
          non_zero_ind = np.where(npheight>high)[0]
          print(non_zero_ind)
          while non_zero_ind.shape[0] >= 2:
              result += non_zero_ind[-1] - non_zero_ind[0] - non_zero_ind.shape[0] + 1
              high += 1
              non_zero_ind = np.where(npheight>high)[0]
              
          return result
  ```
  
  numpy를 활용하여, 높이가 상승함에 따라 벽이 존재하는 좌우 인덱스의 차이에 사이의 벽의 개수를 빼주는 방식으로 계싼
  
  But, where 계산비용으로 시간이 여전히 오래걸림 
  
  

- #### Solution 3

  ```python
  # 76 ms	15.7 MB	python3
  # Runtime: 76 ms, faster than 61.75% of Python3 online submissions for Trapping Rain Water.
  # Memory Usage: 15.7 MB, less than 61.19% of Python3 online submissions for Trapping Rain Water.
  
  from typing import List
  class Solution:
      def trap(self, height: List[int]) -> int:
          result = 0
          
          left, right = 0 , len(height) - 1
          left_max, right_max = height[left], height[right]
          
          while left < right:
              left_max, right_max = max(left_max, height[left]), max(right_max, height[right])
              
              if left_max <= right_max:
                  result += left_max - height[left]
                  left += 1
              else:
                  result += right_max - height[right]
                  right -= 1
          return result
  ```

  Two Pointer를 활용하여, 좌우에서 포인터가 움직이기 시작하여, 작은 쪽에서 큰 쪽을 향해 나아가며,

  움직일 때마다 Max 벽 - 현재 포인터 벽 만큼 물이 차있는걸 계산하며 움직임 

​    

- #### Point

  문제를 단순화하여 Two Pointer로 처리 