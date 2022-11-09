此题与LeetCode 409题相似，都是寻找字符，重新组成回文。但难度在于：
1) 此题为数字，需按位提取
2) 此题结果要求值最大的数字，相较于字符串长度，本题目标值有且只有一个，需要按大小排序提取并排列

```
n= 888897712133

def maxnum(number:int):

    #前期处理，得到数字与相应个数的哈希表，和一个按逆序排列的数字列表
    import collections
    list_n = list(map(int,(str(number))))   #数字转换为数字列表
    if len(list_n) == 0 or len(list_n) == 1:
        return n
    dn = dict(collections.Counter(list_n))  #数字对应个数的哈希表
    lkey = list(dn.keys())
    lkey.sort(reverse=True) #需要由大到小排列。由于字典dn是无序的，所以设此列表用于提取数字并排列。此处，list.sort()返回值为对象，直接使用list即可。
    
    #开始排列，大的值靠前（需要对称，故取一半的值）
    listn= []
    for i in lkey:
        if dn[i] % 2 == 1:
            max_n = i   #找到最大的数量为奇数的值，取出一个这个数放在中间
            break
    for i in lkey:
        listn += [i] * (dn[i] // 2)
    ll = listn + [max_n] + listn[::-1]
    max_num = int(''.join(map(str,ll))) #数字列表转数字

    return max_num

print(maxnum(n))
```
