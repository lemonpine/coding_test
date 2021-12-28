# Problem 팰린드롬 연결 리스트

https://leetcode.com/problems/palindrome-linked-list/



- #### Problem : 연결리스트(Linked List)가 팰린드롬인지 판단

  

  ##### ## Linked List 설명 ##

  ```python
  # Definition for singly-linked list.
  class ListNode:
      def __init__(self, val=0, next=None):
          self.val = val
          self.next = next
  ```

  Linked List는 자신의 값(val)과 다음 연결리스트(next)로 이루어진 객체 

  ![그림](https://assets.leetcode.com/uploads/2021/03/03/pal1linked-list.jpg)

  

  Example 1:

    ```
  Input: head = [1,2,2,1]
  Output: true
    ```

  Example 2:

    ```
  Input: head = [1,2]
  Output: false
    ```

  ----------------------------------------------------

  

- #### Solution 1

  ```python
  # 824 ms	47.2 MB	python3
  # Runtime: 824 ms, faster than 53.68% of Python3 online submissions for Palindrome Linked List.
  # Memory Usage: 47.2 MB, less than 43.36% of Python3 online submissions for Palindrome Linked List.
  from typing import Optional
  class Solution:
      def isPalindrome(self, head: Optional[ListNode]) -> bool:
          num_list = []
          node = head
          while node:
              num_list.append(node.val)
              node = node.next
          
          return num_list == num_list[::-1]
  ```
  
  연결 리스트를 기본 리스트로 변형한 후 팰린드롬인지 판별하는 방식으로 직관적이지만,
  
  list로 변환하는 과정에서 불필요한 처리 수행
  
  ​    
  
- #### Solution 2

  ```python
  # 804 ms	39.2 MB	python3
  # Runtime: 804 ms, faster than 65.37% of Python3 online submissions for Palindrome Linked List.
  # Memory Usage: 39.2 MB, less than 87.14% of Python3 online submissions for Palindrome Linked List.
  from typing import Optional
  class Solution:
      def isPalindrome(self, head: Optional[ListNode]) -> bool:
          
          while head == None or head.next == None:
              return True
          
          # head.next -> one_jump_node is required one more step
          one_jump_node, two_jump_node = head.next, head
          while two_jump_node.next and two_jump_node.next.next:
              two_jump_node = two_jump_node.next.next
              one_jump_node = one_jump_node.next
          
          # Reverse
          prev = None
          while one_jump_node:
              tmp1 = one_jump_node.next
              one_jump_node.next = prev
              prev = one_jump_node
              one_jump_node = tmp1
          
          # half of node vs rever half of node
          while prev:
              if head.val != prev.val:
                  return False
              head, prev = head.next, prev.next
         
          return True
  ```
  
  리스트 변환이 아닌 연결리스트 그 구조 자체를 유지하며, 팰린드롬인지 판단
  
  중간지점 찾기 -> 중간지점 이후 값들을 Reverse 하기 -> 앞의 절반과 뒤의 절반의 Reverse값이 동일한지 판단 
  
  

- #### Point

  연결 리스트에 대한 이해와 while LinkedList: or while LinkedList.next: 방식의 접근을 통해

  다음 객체를 찾아나가는 리스트에서 for문의 순차적 접근과 방식에 대한 이해