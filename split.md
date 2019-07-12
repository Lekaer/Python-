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
print(str.split(' ', 1 )[1]) # 输出第一个
```
运行结果如下：
```
['Line1-abcdef', 'Line2-abc', 'Line4-abcd']
['Line1-abcdef', '\nLine2-abc \nLine4-abcd']
Line1-abcdef
```
