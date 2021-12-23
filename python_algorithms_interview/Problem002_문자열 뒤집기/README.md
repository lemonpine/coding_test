# Problem 문자열 뒤집기 

https://leetcode.com/problems/reverse-string/



- #### Problem : 문자열을 뒤집는 함수를 작성 

  *리턴 없이 리스트 내부를 직접 조작

  Example 1:

  ```
  Input: s = ["h","e","l","l","o"]
  Output: ["o","l","l","e","h"] 
  ```
  
Example 2:
  
```
  Input: s = ["H","a","n","n","a","h"]
  Output: ["h","a","n","n","a","H"]
  ```
  
  ---------------------

  

- #### Solution 1

  ```python
  # 200 ms	18.5 MB	python3
  # Runtime: 200 ms, faster than 65.19% of Python3 online submissions for Reverse String.
  # Memory Usage: 18.5 MB, less than 83.58% of Python3 online submissions for Reverse String.
  
  class Solution:
      def reverseString(self, s: List[str]) -> None:
          """
          :type s: List[str]
          :rtype: None Do not return anything, modify s in-place instead.
          """
          
          s[:] = s[::-1]
  ```

  reverse()를 이용하는 방식으로, 문자열 슬라이싱을 활용 

  **※ s = s[::-1]의 경우 s라는 새로운 변수를 할당하는 방면, s[:] == s[::-1] 기존 s를 변경**

  

- #### Solution 2

  ```python
  # 212 ms	18.6 MB	python3
  # Runtime: 212 ms, faster than 28.68% of Python3 online submissions for Reverse String.
  # Memory Usage: 18.6 MB, less than 44.19% of Python3 online submissions for Reverse String.
  
  class Solution:
      def reverseString(self, s: List[str]) -> None:
          """
          :type s: List[str]
          :rtype: None Do not return anything, modify s in-place instead.
          """
          c = int(len(s)/2)
          for n in range(c):
              s[n], s[len(s)-n-1] = s[len(s)-n-1], s[n]
  ```

  좌우 양쪽 끝에서 값을 바꿔주는 코드



- #### Point

  python list 값 할당 방식의 차이점 s / s[:]

  two pointer를 직접 활용하지는 않았지만 좌우 동시처리