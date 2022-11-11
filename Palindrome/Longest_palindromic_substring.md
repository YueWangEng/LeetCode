## 暴力算法（会超时）
```python3
class Solution:
    def longestPalindrome(self, s: str) -> str:
        def palin(s1):  #自定义回文判断函数
            pass
        n = len(s)
        if n == 0 or n == 1:
            return s
        else:
            length, begin, ennd = 0, 0, 1
            for i in range (0,n-1): #从前到后选定字符，判断该字符与其后面连续字符组成的子串是否为回文
                for j in range(i+1, n+1):
                    if palin(s[i:j]) and (j-i > length):
                        begin, end, length = i, j, j-i
                
        return s[begin:end]
```
