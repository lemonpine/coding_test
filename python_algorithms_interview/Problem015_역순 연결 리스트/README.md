# Problem 역순 연결 리스트

https://leetcode.com/problems/reverse-linked-list/



- #### Problem : 연결리스트(Linked List)를 역순으로 변경

  

  Example 1:

    ```
  Input: head = [1,2,3,4,5]
  Output: [5,4,3,2,1]
    ```

  Example 2:

    ```
  Input: head = [1,2]
  Output: [2,1]
    ```

  Example 3:

  ```
  Input: head = []
  Output: []
  ```

  --------------------------------------------------

  

- #### Solution 1

  ```python
  # 28 ms	15.6 MB	python3
  # Runtime: 28 ms, faster than 96.37% of Python3 online submissions for Reverse Linked List.
  # Memory Usage: 15.6 MB, less than 76.59% of Python3 online submissions for Reverse Linked List.
  from typing import Optional
  class Solution:
      def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
          
          reverse = None
          while head:
              tmp = head.next
              head.next = reverse
              reverse = head
              head = tmp
          
          return reverse
  ```

  연결리스트를 차례로 접근할 때, 현재 연결리스트를 next로 연결하는 것이 아닌, 해당 연결리스트의 next에

  지금까지 앞에 있었던 연결리스트들을 연결하는 방식 

  ​    

- #### Point

  값을 임시로 할당하고, 모든 처리 이후 다시 기존 값에 할당시키는 방식의 구현