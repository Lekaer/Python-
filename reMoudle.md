# python re模块常用方法
>re, regular expressin的缩写，即正则表达式
## **正则表达式-主要语法**
| 模式 | 描述 |
| :------------ | :------------- |
| \d | 匹配一个数字 |
| \w | 匹配一个字母数字及下划线 |
| \s | 匹配任意空白符 |
| ? | 匹配0个或1个字符 |
| * | 匹配0个或多个字符 |
| + | 匹配1个或多个字符 |
| {} | 表示前面正则表达式的重复次数,例如'o{2}'可以匹配'food' |
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
| {n,} | 至少匹配n次,n为非负整数 |
| {n,m} | 最少匹配n次最多匹配m次,n<=m均为非负整数 |

| 修饰符 | 描述 |
| :------------ | :------------- |
| re.I | 使匹配对大小写不敏感 |
| re.M | 多行匹配，影响 ^ 和 $ |
| re.S | 使 . 匹配包括换行在内的所有字符 |
| ... | ... |
## **re模块-常用函数**
+ ### **re.match和re.search**

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

+ ### **re.compile**

>将正则表达式模式编译为正则表达式对象，可以使用其match（）和search（）方法进行匹配
>compile()函数会把一个表达式字符串转化成为一个RegexObject

语法：
>re.compile(pattern, flags=0)

**实例1**

参考re.findall的实例1

**实例2**
```
import re 
# Precompile the patterns
regexes = [re.compile(p) for p in ['this', 'that']]
text = "Does this text match the pattern?"
print 'Text: %r\n' % repr(text)

for regex in regexes:
    print 'Seeking "%s"->' % regex.pattern,     
    if regex.search(text):
        print 'match!'
    else:
        print 'no match'
```
执行结果如下：
>Text: "'Does this text match the pattern?'"

>Seeking "this"-> match!
>Seeking "that"-> no match

说明：
>repr(object)函数返回一个对象的string格式


+ ### **re.findall**

>在字符串中找到正则表达式所匹配的所有子串，并返回一个列表，如果没有找到匹配的，则返回空列表。

语法：
>findall(pattern, string, flags=0)

参数说明：

| 参数 | 描述 |
| :------------ | :------------- |
| pattern | 匹配的正则表达式RE |
| string | 待匹配的字符串 |
| flags | -- |

**实例1**
```
>>> import re
>>> s = "adfad asdfasdf asdfas asdfawef asd adsfas "
 
>>> reObj1 = re.compile('((\w+)\s+\w+)')
>>> reObj1.findall(s)
[('adfad asdfasdf', 'adfad'), ('asdfas asdfawef', 'asdfas'), ('asd adsfas', 'asd')]
 
>>> reObj2 = re.compile('(\w+)\s+\w+')
>>> reObj2.findall(s)
['adfad', 'asdfas', 'asd']
 
>>> reObj3 = re.compile('\w+\s+\w+')
>>> reObj3.findall(s)
['adfad asdfasdf', 'asdfas asdfawef', 'asd adsfas']
```
说明：

>1.当给出的正则表达式中带有多个括号时，列表的元素为多个字符串组成的tuple，tuple中字符串个数与括号对数相同，字符串内容与每个括号内的正则表达式相对应，并且排放顺序是按括号出现的顺序。

>2.当给出的正则表达式中带有一个括号时，列表的元素为字符串，此字符串的内容与括号中的正则表达式相对应（不是整个正则表达式的匹配内容）。

>3.当给出的正则表达式中不带括号时，列表的元素为字符串，此字符串为整个正则表达式匹配的内容。

**实例2**
```
>>> a = "one two three four five six"
>>> b = re.findall("(one)|(two)|(three)|(four)|(five)|(six)",a)#加上了"|"号
>>> print(b)
[('one', '', '', '', '', ''), ('', 'two', '', '', '', ''),
('', '', 'three', '', '', ''),('', '', '', 'four', '', ''),
('', '', '', '', 'five', ''),('', '', '', '', '', 'six')]
```

说明：
>1.这个结果是因为按组匹配所以有元组，每个元组都有六个元素。

>2.因为是条件匹配，列了六种匹配条件，于是findall匹配六次，结果列表有六个元素。

>3.又因为每次匹配只能用一种条件，所以按组匹配结果列表中的每个元组只有一组有值而其他均为空。

**实例3**
```
>>> x = "3 min 46 sec 300 ms"
#分秒毫秒的提取
>>> print(re.findall(r"(\d{0,}) (min|sec|ms)",x))
[('3', 'min'), ('46', 'sec'), ('300', 'ms')]
```

- ### **re.split**
>按照指定的 pattern 格式，分割 string 字符串，返回一个分割后的列表。

语法：
>re.split(pattern, string, maxsplit=0, flags=0)

maxsplit 指定最大分割次数，默认为0，全部分割

**实例**
```
>>> import re
>>> line = 'aaa bbb ccc;ddd   eee,fff'
>>> line
'aaa bbb ccc;ddd   eee,fff'
```
单字符切割
```
>>> re.split(r';',line)
['aaa bbb ccc', 'ddd\teee,fff']
```
两个字符以上切割需要放在[]中
```
>>> re.split(r'[;,]',line)
['aaa bbb ccc', 'ddd\teee', 'fff']
```
所有空白字符切割
```
>>> re.split(r'[;,\s]',line)
['aaa', 'bbb', 'ccc', 'ddd', 'eee', 'fff']
```
使用括号捕获分组，默认保留分割符
```
>>> re.split(r'([;])',line)
['aaa bbb ccc', ';', 'ddd\teee,fff']
```
不想保留分隔符，以（?:...）的形式指定
```
>>> re.split(r'(?:[;])',line)
['aaa bbb ccc', 'ddd\teee,fff']
```


- ### **re.sub**
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
