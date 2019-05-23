# python re模块常用方法
>re, regular expressin的缩写，即正则表达式
## **正则表达式-主要语法**
| 模式 | 描述 |
| :------------ | :------------- |
| \d | 匹配一个数字 |
| \w | 匹配一个字母数字及下划线 |
| ? | 匹配0个或1个字符 |
| * | 匹配0个或多个字符 |
| + | 匹配1个或多个字符 |
| {} | 表示前面正则表达式的重复次数 |
| . | 匹配任意字符(默认除换行符) |
| ^ | 匹配字符串的开头 |
| $ | 匹配字符串的末尾 |
| () | 匹配括号内的表达式，表示一个组 |
| [..] | 匹配一组字符:[ab]匹配a或b |
| [^..] | 匹配一组字符:[^ab]匹配a,b之外的字符 |
| \1...\9 | 匹配第n个分组的内容 |

| 实例 | 描述 |
| :------------ | :------------- |
| [0-9] | 匹配任何数字，与\d等价 |
| [^0-9] | 匹配除了数字外的字符 |
| [a-z] | 匹配任何小写字母 |

| 修饰符 | 描述 |
| :------------ | :------------- |
| re.I | 使匹配对大小写不敏感 |
| re.M | 多行匹配，影响 ^ 和 $ |
| re.S | 使 . 匹配包括换行在内的所有字符 |
| ... | ... |
## **re模块-常用函数**
+ re.match和re.search

match匹配字符串的开始，匹配成功返回matchobject，否则返回none

search匹配整个字符串，匹配成功返回matchobject，否则返回none

例如对于字符串"asdfabbbb"
```
>>> m=re.match("^ab+","asdfabbbb")
>>> print m
None
>>> m=re.match("ab+","asdfabbbb")
>>> print m
None
```
re.match从字符串的起始位置按正则表达式匹配，而re.search则不限制位置
```
>>> m=re.search("^ab+","asdfabbbb")
>>> print m
None
>>> m=re.search("ab+","asdfabbbb")
>>> print m
<_sre.SRE_Match object at 0x011B1988>
>>> print m.group()
abbbb
```
- re.findall
- re.split
- re.sub
>match和search的区别:
>search和findall的区别:
