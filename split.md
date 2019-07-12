## split用法总结
+ ### split()
+ ### strip()与split()
+ ### split()与re.split()
## 1 split()
>通过指定分隔符对字符串进行切片,返回分割后的字符串列表。

语法：

>str.split(str="", num=string.count(str))

+ str -- 分隔符，默认为所有的空字符，包括空格、换行(\n)、制表符(\t)等。

+ num -- 分割次数。默认为 -1, 即分隔所有。

**实例1**
```
str = "Line1-abcdef \nLine2-abc \nLine4-abcd";
print(str.split())           # 以空格为分隔符，包含 \n
print(str.split(' ', 1 ))    # 以空格为分隔符，分隔成两个
print(str.split(' ', 2 )[1]) # 分隔两次，输出第二个
```
运行结果如下：
```
['Line1-abcdef', 'Line2-abc', 'Line4-abcd']
['Line1-abcdef', '\nLine2-abc \nLine4-abcd']
Line2-abc
```

**实例2**
```
>>> str="hello boy<[www.doiido.com]>byebye"

>>> print str.split("[")[1].split("]")[0]
www.doiido.com

>>> print str.split("[")[1].split("]")[0].split(".")
['www', 'doiido', 'com']
```
**os.path.split('PATH')**

说明：
+ PATH指一个文件的全路径作为参数

+ 如果给出的是一个目录和文件名，则输出路径和文件名

+ 如果给出的是一个目录名，则输出路径和为空文件名

## 2 strip()与spilt()
+ strip()函数

>用于移除字符串头尾指定的字符（默认，空格包括'\n','\r','\t',' '）或字符序列，返回移除字符串头尾指定的字符生成的新字符串。(不能删除中间部分的字符)

**实例**
```
>>> a = '     123'
>>> a.strip()
'123'

>>> a='\t\tabc'
>>> a.strip()
'abc'

>>> a = 'sdff\r\n'
>>> a.strip()
'sdff'
```
```
>>>str = "123abcrunoob321"
>>>str.strip( '12' )      # 字符序列为 12
3abcrunoob3
```
+ strip().split()

**实例**
```
>>> str = '  www.google.com.cn '
>>> str_split = str.strip().split('.')
['www','google','com','cn']

>>> str_split[::-1]
['cn','com' 'google','www']
>>> str_split[:-1]
['www','google','com']
```

## 3 str.split()与re.split()
+ str.split不支持正则及多个切割符号，不感知空格的数量

例如：
```
>>> s1="aa bb  cc"
>>> s1.split(' ')
['aa', 'bb', '', 'cc']
```
+ re.split，支持正则及多个字符切割



