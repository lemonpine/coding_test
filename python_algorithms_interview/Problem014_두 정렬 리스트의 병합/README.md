# Problem 두 정렬 리스트의 병합

https://leetcode.com/problems/merge-two-sorted-lists/



- #### Problem : 두 인풋을 내림차순으로 하나의 연결 리스트로 병합

  

  Example 1:

    ```
  Input: list1 = [1,2,4], list2 = [1,3,4]
  Output: [1,1,2,3,4,4]
    ```

  Example 2:

    ```
  Input: list1 = [], list2 = []
  Output: []
    ```

  Example 3:

  ```
  Input: list1 = [], list2 = [0]
  Output: [0]
  ```

  --------------------------------------------------

  

- #### Solution 1

  ```python
  # 32 ms	14.3 MB	python3
  # Runtime: 32 ms, faster than 91.95% of Python3 online submissions for Merge Two Sorted Lists.
  # Memory Usage: 14.3 MB, less than 31.91% of Python3 online submissions for Merge Two Sorted Lists.
  from typing import Optional
  class Solution:
      def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
          head, tail = None, None
          
          if list1 is None:
              return list2
          if list2 is None:
              return list1
          
          while list1 and list2:
              if list1.val <= list2.val:
                  tmp = list1.next
                  list1.next = None
                  if head == None:
                      tail = list1
                      head = tail
                  else:
                      tail.next = list1
                      tail = list1
                  list1 = tmp
              else:
                  tmp = list2.next
                  list2.next = None
                  if head == None:
                      tail = list2
                      head = tail
                  else:
                      tail.next = list2
                      tail = list2
                  list2 = tmp
          if list1:
              tail.next = list1
          elif list2:
              tail.next = list2
          return head
  ```

  직관적인 풀이로 두 연결 리스트의 값 중 작은 값을 같는 연결리스트를 순차적으로 병합하는 방식을 취함

  코드가 굉장히 길며, 아래의 재귀를 이용한 풀이보다 복잡하지만 오히려 성능은 좋았는데,

  그 이유는 한쪽 리스트만 남은 경우에 대해 한 객체에 대한 반복 접근이 아닌, 한쪽 리스트를 한번에 

  연결하는 구현이 있기 때문

  ​    

- #### Solution 2

  ```python
  # 40 ms	14.5 MB	python3
  # Runtime: 40 ms, faster than 49.42% of Python3 online submissions for Merge Two Sorted Lists.
  # Memory Usage: 14.5 MB, less than 31.91% of Python3 online submissions for Merge Two Sorted Lists.
  from typing import Optional
  class Solution:
      def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
          
          if list1 is None or (list2 and list1.val > list2.val):
              list1, list2 = list2, list1
          if list1:
              list1.next = self.mergeTwoLists(list1.next, list2)
          return list1
  ```
  
  반복적인 처리를 재귀를 활용하여 구현 
  
  코드가 굉장히 간단하며, 사실 재귀의 경우 for문과 같은 순차적접근보다 느린 방식이지만 연결리스트 객체에 접근할 때는 좋은 성능을 가진 접근법
  
  

- #### Point

  동일한 인풋구조에 동일한 처리를 반복할 경우 재귀(recursion) 함수를 (self.함수이름) 사용하는 것이

  구조를 간단히 하며, 좋은 성능을 가짐