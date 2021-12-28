# Problem 주식을 사고팔기 가장 좋은 시점

https://leetcode.com/problems/best-time-to-buy-and-sell-stock/



- #### Problem : 연속된 숫자 리스트를 입력 받았을 때, 주식을 사고 팔아 가장 높은 마진의 기대값을 구하시오

  

  Example 1:

    ```
  Input: prices = [7,1,5,3,6,4]
  Output: 5
   # Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
   # Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.
    ```

  Example 2:

    ```
  Input: prices = [7,6,4,3,1]
  Output: 0
   # Explanation: In this case, no transactions are done and the max profit = 0.
    ```

  ----------------------------------------------------

  

- #### Solution 1

  ```python
  # 9900 ms	42 MB	python3
  # Runtime: 9900 ms, faster than 5.00% of Python3 online submissions for Best Time to Buy and Sell Stock.
  # Memory Usage: 42 MB, less than 5.26% of Python3 online submissions for Best Time to Buy and Sell Stock.
  from typing import List
  class Solution:
      def maxProfit(self, prices: List[int]) -> int:
          result = 0
          min_ind = len(prices)
          while min_ind > 0:
              min_ind = prices[:min_ind].index(min(prices[:min_ind]))
              max_ind = prices[min_ind:].index(max(prices[min_ind:]))
              print('min_ind', min_ind, 'max_ind', max_ind + min_ind)
              result = max(result, prices[min_ind + max_ind] - prices[min_ind])
  #             min_ind -= 1
  
          return result
  ```
  
  가장 작은 값을 구한 후, 그 이후 가장 큰 값을 구하여 차이 계산
  
  그 이전 가장 작은 값을 구한 후, 그 이후 가장 큰 값을 구하여 차이 계산하는 방법으로 
  
  직관적으로 구현하려 했으나, 굉장히 낮은 성능을 보임 (max/min & index 함수 사용 등)
  
  ​    
  
- #### Solution 2

  ```python
  # 1020 ms	26.2 MB	python3
  # Runtime: 1020 ms, faster than 69.03% of Python3 online submissions for Best Time to Buy and Sell Stock.
  # Memory Usage: 26.2 MB, less than 5.26% of Python3 online submissions for Best Time to Buy and Sell Stock.
  import sys
  from typing import List
  class Solution:
      def maxProfit(self, prices: List[int]) -> int:
        
          # local high and low point search
          p = prices[0]
          local_high, local_low = [], []
          bup = False
          for i in range(1, len(prices)):
              if p < prices[i]:
                  if not bup:
                      local_low.append(i - 1)
                      bup = True
              else:
                  if bup:
                      local_high.append(i - 1)
                      bup = False
              p = prices[i]
          if bup:
              local_high.append(i)
  
  #         print(local_high, local_low)
  
          result = 0
          min_price = sys.maxsize
          for i in range(len(local_high)):
              min_price = min(min_price, prices[local_low[i]])
  #             print(min_price, local_high[i])
              result = max(result, prices[local_high[i]] - min_price)
          
          return result
  ```
  
  증가상태, 감소상태를 기준으로 극소/극대 값을 갖는 인덱스를 구한 후
  
  극소와 극대값의 차이의 최대값을 구하는 방식으로 위의 해결 방식에 비해 비효율적인 함수를 적게 사용하였으나
  
  for문을 2번 수행해야 해서 조금 아쉬운 풀이법
  
  
  
- #### Solution 3

  ```python
  # 944 ms	25 MB	python3
  # Runtime: 944 ms, faster than 90.58% of Python3 online submissions for Best Time to Buy and Sell Stock.
  # Memory Usage: 25 MB, less than 81.89% of Python3 online submissions for Best Time to Buy and Sell Stock.
  import sys
  from typing import List
  class Solution:
      def maxProfit(self, prices: List[int]) -> int:
        
          result = 0
          min_price = sys.maxsize
          prev_price = 0
          for price in prices:
              if min_price > price:
                  min_price = price
              if prev_price < price:
                  result = max(result, price - min_price)
              prev_price = price
          return result
  ```

  위의 극대/극소값을 찾는 for문과 최대 마진을 찾는 for문을 통합하여 한번에 처리하는 방식의 구현

  

- #### Point

  sys.maxsize -> int값이 가질 수 있는 가장 큰 값을 의미