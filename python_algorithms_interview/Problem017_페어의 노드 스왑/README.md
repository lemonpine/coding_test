# Problem 페어의 노드 스왑

https://leetcode.com/problems/swap-nodes-in-pairs/



- #### Problem : 순차적으로 두개의 값을 스왑한 후 return

  

  Example 1:

    ```
  Input: head = [1,2,3,4]
  Output: [2,1,4,3]
    ```

  Example 2:

    ```
  Input: head = []
  Output: []
    ```

  Example 3:

  ```
  Input: head = [1]
  Output: [1]
  ```

  --------------------------------------------------

  

- #### Solution 1

  ```python
  # 32 ms	14.4 MB	python3
  # Runtime: 32 ms, faster than 63.44% of Python3 online submissions for Swap Nodes in Pairs.
  # Memory Usage: 14.4 MB, less than 16.01% of Python3 online submissions for Swap Nodes in Pairs.
  from typing import Optional
  class Solution:
      def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:
          
          if head is None or head.next is None:
              return head
          
          result, tail = None, None
          while head and head.next:
              First = ListNode(head.next.val)
              Second = ListNode(head.val)
              First.next = Second
              head = head.next.next
              if result is None:
                  tail = First
                  result = tail
                  tail = tail.next
              else:
                  tail.next = First
                  tail = tail.next.next
  
          tail.next = head
          
          return result
          
  ```

  연결리스트를 2칸 씩 움직이며, 앞의 2개를 스왑하여 결과값에 연결하는 방식이지만

  불필요하게 앞의 2개의 값을 임시로 반복하여 할당시키기에 불필요 처리가 존재

  

- #### Solution 2

  ```python
  # 24 ms	14.1 MB	python3
  # Runtime: 24 ms, faster than 95.81% of Python3 online submissions for Swap Nodes in Pairs.
  # Memory Usage: 14.1 MB, less than 92.58% of Python3 online submissions for Swap Nodes in Pairs.
  from typing import Optional
  class Solution:
      def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:
          
          if head and head.next:
              tmp = head.next
              head.next = self.swapPairs(tmp.next)
              tmp.next = head
              return tmp
          return head
  
  ```

  재귀를 이용하여 스왑된 형태를 순차적으로 할당 후 다음처리하는 것이 아닌,

  가장 마지막 연결리스트에서 부터 차례로 앞에 붙여나가는 식의 풀이

  

- #### Point

  문제를 반복적인 구조로 단순화시키고 이를 재귀를 활용하여 구현