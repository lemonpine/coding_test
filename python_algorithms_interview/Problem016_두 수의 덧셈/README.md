# Problem 두 수의 덧셈

https://leetcode.com/problems/add-two-numbers/



- #### Problem : 연결 리스트로 이루어진 두 수의 덧셈

  *앞의 연결리스트가 일의 자리부터 시작하여 다음 연결리스트들이 10의 n-1승 자리수를 의미

  

  Example 1:

    ```
  Input: l1 = [2,4,3], l2 = [5,6,4]
  Output: [7,0,8]
   # Explanation: 342 + 465 = 807.
    ```

  Example 2:

    ```
  Input: l1 = [0], l2 = [0]
  Output: [0]
    ```

  Example 3:

  ```
  Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
  Output: [8,9,9,9,0,0,0,1]
  ```

  --------------------------------------------------

  

- #### Solution 1

  ```python
  # 72 ms	14.4 MB	python3
  # Runtime: 72 ms, faster than 53.76% of Python3 online submissions for Add Two Numbers.
  # Memory Usage: 14.4 MB, less than 45.07% of Python3 online submissions for Add Two Numbers.
  from typing import Optional
  class Solution:
      def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
          
          head, tail = None, None
          tmp = 0
          while l1 and l2:
              tmp, val = int((l1.val + l2.val + tmp) / 10), (l1.val + l2.val + tmp) % 10
              if head is None:
                  tail = ListNode(val)
                  head = tail
              else:
                  tmp_node = ListNode(val)
                  tail.next = tmp_node
                  tail = tmp_node
              l1, l2 = l1.next, l2.next
          
          while l1:
              tmp, val = int((l1.val + tmp) / 10), (l1.val + tmp) % 10
              tmp_node = ListNode(val)
              tail.next = tmp_node
              tail = tmp_node
              l1 = l1.next
  
          while l2:
              tmp, val = int((l2.val + tmp) / 10), (l2.val + tmp) % 10
              tmp_node = ListNode(val)
              tail.next = tmp_node
              tail = tmp_node
              l2 = l2.next
          
          if tmp:
              tail.next = ListNode(tmp)
          
          return head
  ```

  논리 회로의 전가산기(Full Adder)와 유사한 형태로 작은 자리의 숫자부터 더한 후 만약 10을 넘어가면 

  다음 자리수에 1을 추가로 더해주는 (carry-in)의 구현

  

- #### Solution 2

  ```python
  # 56 ms	14.4 MB	python3
  # Runtime: 56 ms, faster than 98.96% of Python3 online submissions for Add Two Numbers.
  # Memory Usage: 14.4 MB, less than 45.07% of Python3 online submissions for Add Two Numbers.
  from typing import Optional
  class Solution:
      def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
          
          head, tail = None, None
          tmp = 0
          while l1 or l2:
              val = tmp
              if l1:
                  val += l1.val
                  l1 = l1.next
              if l2:
                  val += l2.val
                  l2 = l2.next
              tmp = int(val/10)  
              val -= tmp*10
              
              if head is None:
                  tail = ListNode(val)
                  head = tail
              else:
                  tmp_node = ListNode(val)
                  tail.next = tmp_node
                  tail = tmp_node
  
          if tmp:
              tail.next = ListNode(tmp)
          
          return head
  ```

  위의 풀이를 더욱 간단하게 고친것으로 여러개의 while문을 사용하는 것이 아닌, 하나의 while문으로 통합하여

  구조를 간단하게 고친 후 성능 향상

  

- #### Point

  