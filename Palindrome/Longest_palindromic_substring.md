### 法1: 暴力算法（会超时）
判断每一个出现的子串，找到最大的。

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
            for i in range (0,n-1): 
                for j in range(i+1, n+1):
                    if palin(s[i:j]) and (j-i > length):    #从前到后选定字符，判断该字符与其后面连续字符组成的子串是否为回文
                        begin, end, length = i, j, j-i
                
        return s[begin:end]
```
或使用
```python3
def longestPalindrome(self, s: str) -> str:
        n = len(s)
        if n == 0 or n == 1:
            return s
        else:
            for i in range (n-1,0,-1):
                for j in range(n-i):
                    sn = s[j:i+j+1] #按子串长度从大到小查找，较前一种算法，一旦找到长的子串，就立刻退出，不再寻找短的子串。能解决大部分，但依然会超时。
                    if sn == sn[::-1]:
                        return sn
            else:
                return s[0]
```


### 法2: 哈希表（枚举法）

