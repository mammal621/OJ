# 208. 实现 Trie (前缀树)

## [题目](https://leetcode-cn.com/problems/implement-trie-prefix-tree/)

实现前缀树，又称字典树

## 代码

    class Trie:
        def __init__(self):
            self.children = [None] * 26
            self.isEnd = False
        
        def searchPrefix(self, prefix: str) -> "Trie":
            node = self
            for ch in prefix:
                ch = ord(ch) - ord("a")
                if not node.children[ch]:
                    return None
                node = node.children[ch]
            return node

        def insert(self, word: str) -> None:
            node = self
            for ch in word:
                ch = ord(ch) - ord("a")
                if not node.children[ch]:
                    node.children[ch] = Trie()
                node = node.children[ch]
            node.isEnd = True

        def search(self, word: str) -> bool:
            node = self.searchPrefix(word)
            return node is not None and node.isEnd

        def startsWith(self, prefix: str) -> bool:
            return self.searchPrefix(prefix) is not None