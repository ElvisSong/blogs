+++
title = "Python数据类型1"
date = 2018-09-10T23:43:34+08:00
categories = ["读书笔记"]
toc = true
author = "ElvisSong"
author_homepage =  "http://elvissong.github.io/life/"
draft = true
+++



## 列表
* 用 [] 表示 ,里面元素可以使多种多样的
* 
| 方法名        | 用法           | 解释  |
| ------------- |:-------------:| -----:|
| append     | alist.append(item) | 列表末尾添加 item 这个项 |
| insert      | alist.insert(i,item)     |   列表索引 i 位置添加 item 这一项 |
| pop | alist.pop()      |    移除并返回列表的最后一项 |
| pop | alist.pop(i)      |    移除并返回列表索引 i 位置的项 |
| sort | alist.sort()      |    对列表进行排序 |
| reverse| alist.reverse()      |    对列表进行反转 |
| del | del alist [i]      |    删除该位置上的元素 |
| index| alist.index(item)      |    返回列表中第一个等于 item 项的索引 |
| count| alist.count(item)      |    返回列表中值为 item 的项的个数 |
| remove| alist.remove(item)      |    删除列表中第一个值为 item 的项 |
* range(a, b, c) 函数 a,起始位置，b,终止位置(不包括)，c 步长
在 python 2.x 中，range(10) 直接返回一个 0~9 的列表；python 3.x 中，返回一个列表对象。使用list(range(10))可得到一个列表。
## 字符串
* 字符串是可以储存零个或多个字母，数字，或其他符号的有序容器。
* 
| 方法名        | 用法           | 解释  |
| ------------- |:-------------:| -----:|
| center     | alist.center(w) | 返回 w 长度的字符串，原字符串居中 |
| count      | alist.count(item) | 返回字符串中出现 item 的次数 |
| ljust     | alist.ljust(w) | 返回 w 长度的字符串，原字符串居左 |
| lower     | alist.lower(w) | 返回 一个字符串，全部小写 |
| rjust     | alist.rjust(w) | 返回 w 长度的字符串，原字符串居右 |
| find     | alist.find(item) | 查询item，返回第一个匹配的索引位置 |
| split     | alist.split(schar) | 以schar 为分隔符，将原字符串分割返回一个列表 |
* 列表和字符串最大的区别就是列表是可修改的而字符串不行，修改字符串必须重新赋值给另一个变量，内存是不会更改的。
## 元组和集合
* 元组里的元素是不可修改的，用 () 扩起，且元组内元素不重复
* 集合是0个或多个无序容器，用 {} 扩起，元素不重复，集合是可变的，set()
* 
| 方法名        | 用法           | 解释  |
| ------------- |:-------------:| -----:|
| union | A.union(B) | 返回集合 A , B 的并集 |
| intersection | A.intersection(B) | 返回集合 A , B 的交集 |
| difference | A.difference(B) | 返回A集合除去 A 与 B 共有的元素（A-（A∩B）） |
| issubset | A.issubset(B) | 判断集合 A 是否是集合 B 的子集|
| add | A.add(item) | 把item 这个元素添加到集合 A 中 |
| remove | A.remove(item) | 从集合 A 中除去 item 这个元素 |

## 字典
* 一般来说就是键值对 {key1: value1, key2: value2} 
* 
| 方法名        | 用法           | 解释  |
| ------------- |:-------------:| -----:|
| keys | Adict.keys() | 以列表的形式返回Adict中的所有 key 值 |
| value | Adict.value() | 以列表的形式返回Adict中的所有 value 值 |
| items | Adict.keys() | 以列表的形式返回Adict中的所有键值对，每个元素是包含键，值的元组 |
| get | Adict.get(key) | 返回 key 所对应的值，如果不存在返回 none |
| get | Adict.get(key , alt) | 返回 key 所对应的值，如果不存在返回 alt |