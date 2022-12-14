## LeetCode 5

### 法1: 暴力算法（会超时）
双层遍历，判断每一个出现的子串，找到最大的。

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

```python3
class Solution:
    def longestPalindrome(self, s: str) -> str:
 
        D = dict()      # 储存之前出现过的字符串的序列
        max_len = 0     # 初始化 回文串的长度
        num = s[0]   # 初始化 回文串

        for i, s1 in enumerate(s):
            if s1 in D:
                # 记录字符出现的索引
                D[s1] += [i]
                # 遍历字符s出现的索引
                for j in D[s1]:
                    # 判断字符s的 j 索引和 i+1 索引之间的字符串是不是回文
                    if s[j:i+1] == s[j:i+1][::-1]:
                        a = s[j:i+1]
                        # 首次满足的长度最大
                        break

                # 判断当前回文的长度和已知的长度比较 大的话更新 max_len 和 num
                if i+1 - j > max_len:
                    max_len = i+1 - j
                    num = a
            else:
                # 添加字符出现的索引
                D[s1] = [i]

        return num
```
以上代码可进行部分改进, 由于新加入的字符位置不需要参与遍历判断，可以先遍历判断再加入。
```python3
for i, s1 in enumerate(s):
    if s1 in D:
        # 遍历字符s出现的索引
        for j in D[s1]:
            # 判断字符s的 j 索引和 i+1 索引之间的字符串是不是回文
            if s[j:i+1] == s[j:i+1][::-1]:
                a = s[j:i+1]
                if i+1 - j > max_len:   # 即刻判断是否为最长回文
                    max_len = i+1 - j
                    num = a
                break
        D[s1] += [i]    #判断以后再加入，否则，在前面都不是回文时，则会出现s[i:i+1]这种单字符情况。
    else:
        # 添加字符出现的索引
        D[s1] = [i]
```

### 法3: 中心扩展法
可进行两次遍历，一次寻找最大奇数回文，一次寻找最大偶数回文，然后再取两者最大。
```python
def longestPalindrome(self, s: str) -> str:
        def palin(s1):
            pass
        if len(s) == 0 or len(s) == 1:
            return s
        else:
            length = 1
            sn = s[0]
            #分奇偶两种形式，奇数单字符向外扩展，偶数双字符向外扩展，可分别进行一次，选取最大的。
            for i in range(len(s)-1):   #偶数情况
                    m = 0
                    while (i >= m) and (i+1+m <len(s)) and (s[i-m] == s[i+1+m]):    #如果s[i] == s[i+1]，则此次开始扩展，直到遇到边界或者两端不相等为止。
                        m += 1
                    if 2*m > length:
                        length = 2*m
                        sn = s[i-m+1: i+1+m]
            for i in range (len(s) -1): #奇数情况
                    k = 1
                    while (i >= k) and (i+k <len(s)) and (s[i-k] == s[i+k]):    #单字符开始扩展，直到遇到边界或者两端不相等为止。
                        k += 1
                    if 2*k-1 > length:
                        length = 2*k - 1
                        sn = s[i-k+1: i+k]
            return sn
```
### 法4: 动态规划法
寻找状态转移方程
