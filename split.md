## split用法总结
+ ### split()
+ ### strip()split()
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




