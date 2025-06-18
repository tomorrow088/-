# -两种思路：第一种，即提交的方法，灵神版：用pairwise遍历相邻的字符，如果对应值前者大于后者，则加前者，如果小于则加-前者，最后一个数值需单独处理，直接加上即可。


ROMAN = {
    'I': 1,
    'V': 5,
    'X': 10,
    'L': 50,
    'C': 100,
    'D': 500,
    'M': 1000,
}
class Solution:
    def romanToInt(self, s: str) -> int:
        ans = 0
        for x, y in pairwise(s):  # 遍历相邻的罗马数字
            x, y = ROMAN[x], ROMAN[y]
            ans += x if x >= y else -x
        return ans + ROMAN[s[-1]]  # 加上最后一个


        
   



第二种：官方精选，将所有发生的可能写入哈希表中，并将特殊情况的字符，即两个字符减一个第一个字符的数值，以便后续相加计算，然后用切片的方法遍历（在切片时，取max（i-1,0），确保索引值有效），然后将遍历的值与创建的哈希表对比并相加即可。# -
def romanToInt(self, s: str) -> int:
    d = {'I': 1, 'IV': 3, 'V': 5, 'IX': 8, 'X': 10, 'XL': 30, 'L': 50, 'XC': 80, 'C': 100, 'CD': 300, 'D': 500,
         'CM': 800, 'M': 1000}
    result = 0
    for i, n in enumerate(s):
        str1 = s[max(i - 1, 0):i + 1]  #作者解析中的2就是用这行代码实现的
        if str1 in d:
            result += d.get(str1)
        else:
            result += d[n]
    return result
