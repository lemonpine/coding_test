# Problem 가장 흔한 단어

https://leetcode.com/problems/most-common-word/



- #### Problem : 금지된 단어를 제외한 가장 흔하게 등장하는 단어를 출력

  

  Example 1:

  ```
  Input: paragraph = "Bob hit a ball, the hit BALL flew far after it was hit.", banned = ["hit"]
  Output: "ball"
   # Explanation: 
   # "hit" occurs 3 times, but it is a banned word.
   # "ball" occurs twice (and no other word does), so it is the most frequent non-banned word in the paragraph. 
   # Note that words in the paragraph are not case sensitive,
  that punctuation is ignored (even if adjacent to words, such as "ball,"), 
  and that "hit" isn't the answer even though it occurs more because it is banned.
  ```
  
  Example 2:
  
  ```
  Input: paragraph = "a.", banned = []
  Output: "a"
  ```
  
  ---------------------
  
  
  
- #### Solution 1

  ```python
  # 40 ms	14.6 MB	python3
  # Runtime: 40 ms, faster than 36.68% of Python3 online submissions for Most Common Word.
  # Memory Usage: 14.6 MB, less than 20.28% of Python3 online submissions for Most Common Word.
  
  import collections
  from typing import List
  class Solution(object):
      def mostCommonWord(self, paragraph, banned):
          """
          :type paragraph: str
          :type banned: List[str]
          :rtype: str
          """
          paragraph = [word for word in ''.join(list(map(lambda x : x if x.isalpha() else " ", paragraph.lower()))).replace("  ", " ").split(" ") if word not in banned]
          return sorted(collections.Counter(paragraph).items(), key = lambda item: item[1], reverse = True)[0][0]
  ```

  한줄로 처리하기 위해 문자이외에 공백처리, 2칸 이상의 공백을 1칸으로 처리, split, 금지단어 제거 후 

  collections 라이브러리 활용 count가 가장 큰 문자를 추출

  

- #### Solution 2

  ```python
  # 28 ms	14.2 MB	python3
  # Runtime: 28 ms, faster than 96.53% of Python3 online submissions for Most Common Word.
  # Memory Usage: 14.2 MB, less than 73.09% of Python3 online submissions for Most Common Word.
  
  import collections
  class Solution:
      def mostCommonWord(self, paragraph: str, banned: List[str]) -> str:
          """
          :type paragraph: str
          :type banned: List[str]
          :rtype: str
          """
          
          word_list = []
          word = ''
          for char in paragraph + '.':
              if char.isalpha():
                  word += char.lower()
              else:
                  if len(word) > 0 and word not in banned:
                      word_list.append(word)
                  word = ''
          
          return sorted(collections.Counter(word_list).items(), key = lambda item: item[1], reverse = True)[0][0]
  ```
  
  불 필요한 한줄처리 대신에 list 변형 없이 문자열을 순차적으로 탐색하며, 공백을 기준으로 단어를 구분 후
  
  금지단어가 제거된 단어리스트 중 가장 흔한 단어를 추출



- #### Point

  문자열을 list로 변환하여 처리하는 것은 시간이 오래걸리기에 가급적 문자열로 처리하며,

  불필요한 한 문장 처리 대신 순차적으로 필요한 작업만 처리