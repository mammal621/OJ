# 拼写单词

## [题目](https://leetcode-cn.com/problems/find-words-that-can-be-formed-by-characters/)

## 代码

    class Solution:
        def countCharacters(self, words: List[str], chars: str) -> int:
            ans = 0
            ch = collections.Counter(chars)
            for w in words:
                cw = collections.Counter(w)
                if all([cw[i] <= ch[i] for i in cw]):
                    ans += len(w)
            return ans
