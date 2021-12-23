# Problem 유효한 팰린드롬

https://leetcode.com/problems/valid-palindrome/



- #### Problem : 주어진 문자열이 팰린드롬(좌우대칭)인지 확인

  *대소문자를 구분하지 않으며, 영문자와 숫자만을 대상으로 한다

  Example 1:

  ```
  Input: s = "A man, a plan, a canal: Panama"
  Output: true
   # Explanation: "amanaplanacanalpanama" is a palindrome.  
  ```

  Example 2:

  ```
  Input: s = "race a car"
  Output: false
   # Explanation: "raceacar" is not a palindrome. 
  ```

  Example 3:

  ```
  Input: s = " "
  Output: true
   # Explanation: s is an empty string "" after removing non-alphanumeric characters.
   # Since an empty string reads the same forward and backward, it is a palindrome.
  ```

  ---------------------

  

- #### Solution 1

  ```python
  # 302 ms 14.7 MB python3
  # Runtime: 408 ms, faster than 5.08% of Python3 online submissions for Valid Palindrome.
  # Memory Usage: 15 MB, less than 37.03% of Python3 online submissions for Valid Palindrome.
  
  class Solution(object):
      def isPalindrome(self, s) -> bool:
  
          s = s.replace(' ', '')
          list_str = list(s)
  
          bPLDR = True
          while len(list_str) > 1:
              if list_str[0].isalnum():
                  if list_str[len(list_str) - 1].isalnum():
                      if list_str[0].upper() != list_str[len(list_str) - 1].upper():
                          bPLDR = False
                          break
                      else:
                          list_str.pop(0)
                          list_str.pop()
                  else:
                      list_str.pop()
              else:
                  list_str.pop(0)           
  
          return bPLDR
  ```

  직관적인 풀이로, 1) 공백제거 2) 좌우 알파벳 여부 확인 3) 좌우 동일한지 여부 체크하는

  굉장히 오래걸리고 해석도 어려운 풀이

  

- #### Solution 2

  ```python
  # 40 ms	14.8 MB	python3
  # Runtime: 40 ms, faster than 89.27% of Python3 online submissions for Valid Palindrome.
  # Memory Usage: 14.8 MB, less than 46.38% of Python3 online submissions for Valid Palindrome.
  
  class Solution(object):
      def isPalindrome(self, s) -> bool:
  
          def isalnum(s):
              return s.isalnum()
          s = ''.join(filter(isalnum,s))
          s = s.lower()
  
          return s[int((len(s)+1)/2):] == s[:int((len(s))/2)][::-1]
  ```

  filter 함수를 이용해 isalnum을 만족하는 문자열만 남긴후

  문자열의 좌 우를 반으로 나눈 후(홀수일 경우 가운데 제외) 좌측을 reverse하였을 시 우측과 동일한지 



- #### Point

  처리속도를 기준으로 봤을 때,  for · while · list 처리 등 보다 **문자열 슬라이싱** 의 작업이 훨씬 빠른성능을 보여줌

  list 변환 후 join or for문의 순차적 접근보다 슬라이싱 기능을 활용할 시 매우 빠른 처리 가능 