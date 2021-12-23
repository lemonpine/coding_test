# Problem 로그 파일 재정렬 

https://leetcode.com/problems/reorder-data-in-log-files/



- #### Problem : 주어진 로그들의 리스트를 기준에 따라 정렬 

  *로그의 가장 앞은 식별자며 그 뒤의 로그에 대해 문자 > 숫자

  *문자는 사전식 순서, 숫자는 Input 그대로 & 로그가 동일할 경우 식별자를 기준으로 정렬

  
  
  Example 1:
  
  ```
Input: logs = ["dig1 8 1 5 1","let1 art can","dig2 3 6","let2 own kit dig","let3 art zero"]
  Output: ["let1 art can","let3 art zero","let2 own kit dig","dig1 8 1 5 1","dig2 3 6"]
 # Explanation:
  The letter-log contents are all different, so their ordering is "art can", "art zero", "own kit dig".
   # The digit-logs have a relative order of "dig1 8 1 5 1", "dig2 3 6".
  ```
  
  Example 2:

  ```
Input: logs = ["a1 9 2 3 1","g1 act car","zo4 4 7","ab1 off key dog","a8 act zoo"]
  Output: ["g1 act car","a8 act zoo","ab1 off key dog","a1 9 2 3 1","zo4 4 7"]
  ```
  
  ---------------------
  
  

- #### Solution 1

  ```python
  # 32 ms	14.4 MB	python3
  # Runtime: 32 ms, faster than 90.46% of Python3 online submissions for Reorder Data in Log Files.
  # Memory Usage: 14.4 MB, less than 66.62% of Python3 online submissions for Reorder Data in Log Files.
  
  class Solution(object):
      def reorderLogFiles(self, logs):
          """
          :type logs: List[str]
          :rtype: List[str]
          """
          type_dict = {}
          type_dict['alpha'] = []
          type_dict['digit'] = []
          for log in logs:
              if log.split(" ")[1].isalpha():
                  type_dict['alpha'].append(log)
              else:
                  type_dict['digit'].append(log)
          
          type_dict['alpha'].sort(key = lambda x :(" ".join(x.split(" ")[1:]), x.split(" ")[0]))
          
          return type_dict['alpha'] + type_dict['digit']
  ```

  문자와 숫자를 분리한 후 sort에 lambda 함수를 key로 하여 정렬하는 것이 핵심

  

- #### Solution 2

  ```python
  # 40 ms	14.4 MB	python3
  # Runtime: 40 ms, faster than 41.74% of Python3 online submissions for Reorder Data in Log Files.
  # Memory Usage: 14.4 MB, less than 38.73% of Python3 online submissions for Reorder Data in Log Files.
  
  class Solution(object):
      def reorderLogFiles(self, logs):
          """
          :type logs: List[str]
          :rtype: List[str]
          """
  
          n, num_list = 0, []
          while n < len(logs):
              if logs[n].split(" ")[1].isdigit():
                  num_list.append(logs.pop(n))
              else:
                  n += 1
                  
          logs.sort(key = lambda x :(" ".join(x.split(" ")[1:]), x.split(" ")[0]))
          
          return logs + num_list
  ```
  
  for문 대신 while문 변형, 메모리 절약을 고민하여 pop을 활용했으나 성능이 좋지 못함 
  
  ※동일한 순차처리라면 while문 보다 for문이 좀더 빠른 처리 가능 



- #### Solution 3

  ```python
  # 32 ms	14.2 MB	python3
  # Runtime: 32 ms, faster than 90.46% of Python3 online submissions for Reorder Data in Log Files.
  # Memory Usage: 14.2 MB, less than 96.94% of Python3 online submissions for Reorder Data in Log Files.
  
  class Solution(object):
      def reorderLogFiles(self, logs):
          """
          :type logs: List[str]
          :rtype: List[str]
          """
          alpha_list, num_list = [], []
          for log in logs:
              if log[log.find(" ") + 1].isalpha():
                  alpha_list.append(log)
              else:
                  num_list.append(log)
                  
          alpha_list.sort(key = lambda x :(x[x.find(" ") + 1:], x[:x.find(" ")]))
          
          return alpha_list + num_list
  ```

  split & join이 속도를 저해할 것으로 판단하여 find를 활용하였으나 큰 효과 없었음



- #### Point

  sorting의 key값으로 lambda를 활용하여 복잡한 작업을 간단하게 처리