# Conclusion of Palindrome

## Related Questions
LeetCode: 5, 9, 409

## Distingushing of Palindrome
### 自定义函数
```python3
def palin(s1):
  m=0
  n=len(s1)-1
  if n == 0:
      return True
  else:
      while m < n:
          if s1[m] == s1[n]:
              m += 1
              n -= 1
          else:
              return False
      else:
          return True                 
```

### 反转判断
以下为序列的反转方法（数字不是序列，字符串属于序列）:

1) 使用-1参数反向读取，`squ_r = squ[::-1]`。例如对于列表ll中，`ll[5:1:-1]`是对于位置5到位置2的元素逆序，也可用遍历`for i in range(5,1,-1)`实现。  
2) 内置函数 reversed()，该函数只是读取，如 `for value in reversed (ll)` 可用于反向读取ll中的项。但该函数不会更改原值，且返回值只为数据类型。若要获取反转后的序列，需用 `squ_r = ''.join(reversed(squ)`。  
3) list内置函数，`list.reverse()`,只适合于list。  
4) 自定义数字反转函数。按位提取，反向获得反转数字。  
