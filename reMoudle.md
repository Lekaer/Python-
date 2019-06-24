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

语法：
>re.match(pattern, string, flags=0)

>re.search(pattern, string, flags=0)

参数说明：

| 参数 | 描述 |
| :------------ | :------------- |
| pattern | 匹配的正则表达式RE |
| string | 要匹配的字符串 |
| flags | 标志位，用于控制正则表达式的匹配方式，如：是否区分大小写，多行匹配等 |

>match匹配字符串的开始，匹配成功返回matchobject，否则返回none

>search匹配整个字符串，匹配成功返回matchobject，否则返回none

例如对于字符串"asdfabbbb"
```
>>> m=re.match("ab+","asdfabbbb")
>>> print(m)
None
>>> m=re.match("as+","asdfabbbb")
>>> print(m)
<re.Match object; span=(0, 2), match='as'>
```
re.match从字符串的起始位置按正则表达式匹配，而re.search则不限制位置
```
>>> m=re.search("^ab+","asdfabbbb")
>>> print(m)
None
>>> m=re.search("ab+","asdfabbbb")
>>> print(m)
<re.Match object; span=(4, 9), match='abbbb'>
>>> print m.group()
abbbb
```
match()和seerch()如果匹配成功则返回一个Match Object对象，还有finditer()。该对象有以下方法：

| 方法/属性 | 作用 |
| :------------ | :------------- |
| group() | 返回被RE匹配的字符串 |
| start() | 返回匹配开始的位置 |
| end() | 返回匹配结束的位置 |
| span() | 返回一个元组包含匹配 (开始,结束) 的位置 |

**实例1**
```
print(re.match('www', 'www.runoob.com').span())  # 在起始位置匹配
print(re.search('com', 'www.runoob.com'))         # 不在起始位置匹配
```
执行结果如下:
>(0, 3)

><re.Match object; span=(11, 14), match='com'>

**实例2**
```
line = "Cats are smarter than dogs" 
searchObj = re.match( r'(.*) are (.*?) .*', line, re.M|re.I)

if searchObj:
   print("searchObj.group(0) : ", searchObj.group(0))
   print("searchObj.group(1) : ", searchObj.group(1))
   print("searchObj.group(2) : ", searchObj.group(2))
else:
   print("Nothing found!!")
```
执行结果如下:
>searchObj.group(0) :  Cats are smarter than dogs

>searchObj.group(1) :  Cats

>searchObj.group(2) :  smarter

+ re.findall和re.finditer

+ re.compile
- re.split
- re.sub
>sub是substitute的所写，表示替换

>主要作用是对于输入的一个字符串，利用正则表达式实现（相对复杂的）字符串替换处理，然后返回被替换后的字符串

语法：
>re.sub(pattern, repl, string, count=0, flags=0)

参数说明：

| 参数 | 描述 |
| :------------ | :------------- |
| pattern | 匹配的正则表达式RE |
| repl | 被替换的字符串,也可以是函数 |
| string | 表示要被处理，要被替换的那个字符串 |
| count | 表示被处理的符合pattern的表达式个数 |

**实例1**
```
inputStr = "hello 111 world 111"
replacedStr = inputStr.replace("111", "222")
print(replacedStr)
```
执行结果如下：
>hello 222 world 222

**实例2**
```
inputStr = "hello 123 world 456"
replacedStr = re.sub("\d+", "222", inputStr)
print(replacedStr)
```
执行结果如下：
>hello 222 world 222

**实例3**
```
import re
def _add_111(str_):
    return str(int(str_.group()) + 111)

if __name__ == '__main__':
    str_ = 'hello 123 world 456 nihao 789'
    print(re.sub('(?P<num>\d+)', _add_111, str_, 2))
```
执行结果如下：
>hello 234 world 567 nihao 789

>match和search的区别:
>search和findall的区别:
