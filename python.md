[TOC]



```sh
python3 -m http.server
```





# 数据类型

### 一、格式化输出

1、输入input

```sh
>>> username = input('请输入用户名：')
请输入用户名：xiaolizi
>>> 
>>> password = input('请输入密码：')
请输入密码：123456
>>> 
>>> print(username)
xiaolizi
>>> print(password)
123456 
```

2、格式化输出

```sh
>>> print("my name is %s,my age is %s" %('xiaolizi',14))
my name is xiaolizi,my age is 14

>>> print("name: {name}, age: {age}".format(name="wang",age=14))
name: wang, age: 14
```



### 二、字符串

#### 0. 字符串颜色控制

有时候我们需要对有用的信息设置不同颜色来达到强调、突出、美观的效果，在命令行或linux终端中，颜色是用转义序列控制的，转义序列是以ESC开头，在代码中用\033表示(ESC的ASCII码用十进制表示就是27，等于用八进制表示的33，\0表示八进制)。注意：颜色控制只在终端界面中有效。

格式：`\033[显示方式;前景色;背景色m正文\033[0m`

| 前景色 | 背景色 | 颜色   |
| ------ | ------ | ------ |
| 30     | 40     | 黑色   |
| 31     | 41     | 红色   |
| 32     | 42     | 绿色   |
| 33     | 43     | 黃色   |
| 34     | 44     | 蓝色   |
| 35     | 45     | 紫红色 |
| 36     | 46     | 青蓝色 |
| 37     | 47     | 白色   |

| 显示方式 | 意义         |
| -------- | ------------ |
| 0        | 终端默认设置 |
| 1        | 高亮显示     |
| 4        | 使用下划线   |
| 5        | 闪烁         |
| 7        | 反白显示     |
| 8        | 不可见       |

例子：

`\033[1;31;40m` 1-高亮显示 31-前景色红色 40-背景色黑色

`\033[0m` 采用终端默认设置，也就是取消颜色设置

比如下面的代码：

```
import time

print('\033[1;31m')
print('登录信息'.center(46, "*"), "\033[0m")
print('\033[34m*HOST:\t', "192.168.1.10")
print('*PORT:\t', "80")
print('*User:\t', "jack")
print('*TIME:\t', time.strftime("%Y-%m-%d %H:%M:%S", time.localtime()))
print('\033[1;31m*' * 50, '\033[0m')
print("\033[32m欢迎登录！\033[0m")
```



#### 1. 分片

```sh
>>>定义字符串str1
>>> str1 = "hello world"
>>> print(str1)
hello world

>>>正向取(从左往右)
>>> str1[1]
'e'

>>> 反向取(负号表示从右往左)
>>> str1[-1]
'd'

>>> 步长：0:9:2,第三个参数2代表步长，会从0开始，每次累加一个2即可，所以会取出索引0、2、4、6、8的字符
>>> str1[0:9:2]
'hlowr'

>>> -1表示从右往左依次取值
>>> str1[::-1]
'dlrow olleh'


>>> 获取字符串的长度，即字符的个数，但凡存在于引号内的都算作字符)
>>> len(str1)
11
```

#### 2. strip, lstrip, rstrip

```sh
>>> str1 = "**tony***"

>>> # 移除左右两边的指定字符
>>> str1.strip('*')
'tony'

>>> # 移除左边的指定字符
>>> str1.lstrip('*')
'tony***'

>>> # 移除右边的指定字符
>>> str1.rstrip('*')
'**tony'
```

#### <font color='red'>3. lower(),upper()</font>

```sh
>>> str2 = 'My nAme is tonY!'

>>> # 将英文字符串全部变小写
>>> str2.lower()
'my name is tony!'

>>> # 将英文字符串全部变大写
>>> str2.upper()
'MY NAME IS TONY!'
```

#### <font color='red'>4. startswith,endswith</font>

```sh
>>> str3 = "i love you"
>>> print(str3)
i love you

#startswith()判断字符串是否以括号内指定的字符开头，结果为布尔值True或False
>>> str3.startswith('i')
True

>>> str3.startswith('o')
False

#endswith()判断字符串是否以括号内指定的字符结尾，结果为布尔值True或False
>>> str3.endswith('u')
True

>>> str3.endswith('o')
False
```

#### 5. split,rsplit

```sh
>>> str5 = 'C:/a/b/c/d.txt'
>>> print(str5)
C:/a/b/c/d.txt
      
#split会按照从左到右的顺序对字符串进行切分，可以指定切割次数
>>> str5.split('/')
['C:', 'a', 'b', 'c', 'd.txt']
      
>>> str5.split('/',1)
['C:', 'a/b/c/d.txt']

#rsplit刚好与split相反，从右往左切割，可以指定切割次数
>>> str5.rsplit('.',1)
['C:/a/b/c/d', 'txt']
```

#### 6. join

```sh
`从可迭代对象中取出多个字符串，然后按照指定的分隔符进行拼接，拼接的结果为字符串
>>> '&'.join('hello')
'h&e&l&l&o'
>>> 
>>> '|'.join(['i','love','you'])
'i|love|you'
```

#### 7. replace

```sh
# 用新的字符替换字符串中旧的字符
>>> str7 = 'my name is xiaoli, my age is 18' 
>>> print(str7)
my name is xiaoli, my age is 18

# 将tony的年龄由18岁改成25岁
>>> str7 = str7.replace('18','25') 
>>> print(str7)
my name is xiaoli, my age is 25

#可以指定修改的个数
>>> str7 = str7.replace('my','MY',1)
>>> print(str7)
MY name is xiaoli, my age is 25
```

#### 8. isdigit,isupper,islower

```sh
>>> str8 = '1314520'
>>> print(str8)
1314520

#判断字符串是否是全小写字母
>>> str8.islower()
False

#判断字符串是否是全数字
>>> str8.isdigit()
True

#判断字符串是否是全大写字母
>>> str8.isupper()
False

#字符串中的单词首字母是否都是大写
>>> str8.istitle()
False
```

#### 9. find

```sh
#find：从指定范围内查找子字符串的起始索引，找得到则返回数字1，找不到则返回-1
>>> msg = 'welcome come to here'
>>> print(msg)
welcome come to here

>>> msg.find('l')
2
 
>>> msg.find('m',0,2)  #在索引为1和2(顾头不顾尾)的字符中查找字符o的索引
-1
```

#### 10. count

```sh
#统计字符在字符串中出现的次数
>>> msg.count('e') 
5 
>>> msg.count('e',1,6) 
1              
```

#### 11. center,ljust,rjust

```sh
>>> # 字符串居中显示，填充
>>> name = 'xiaolizi'

>>> name.center(30,'-')
'-----------xiaolizi-----------'

>>> name.ljust(30,'-')
'xiaolizi----------------------'

>>> name.rjust(30,'-')
'----------------------xiaolizi'
```

   



### 三、列表

#### 1. 添加 

append() 列表尾部追加元素

extend() 一次性在列表尾部添加多个元素

insert() 在指定位置插入元素

```sh
>>> a = ["i","am","xiaoming",18]
>>> print(a)
['i', 'am', 'xiaoming', 18]

>>> a.append('good')
>>> a
['i', 'am', 'xiaoming', 18, 'good']

>>> a.extend(['i','am','god'])
>>> a
['i', 'am', 'xiaoming', 18, 'good', 'i', 'am', 'god']

>>> a.insert(1,'not')
>>> a
['i', 'not', 'am', 'xiaoming', 18, 'good', 'i', 'am', 'god']
```



#### 2. 删除 del,pop,remove

pop()默认删除列表最后一个元素，并将删除的值返回

remove()括号内指名道姓表示要删除哪个元素，没有返回值

```sh
>>> a
['i', 'not', 'am', 'xiaoming', 18, 'good', 'i', 'am', 'god']

>>> del a[0]

>>> a
['not', 'am', 'xiaoming', 18, 'good', 'i', 'am', 'god']

>>> a.pop()
'god'
>>> a
['not', 'am', 'xiaoming', 18, 'good', 'i', 'am']

>>> a.remove("am")
>>> a
['not', 'xiaoming', 18, 'good', 'i', 'am']
```



#### 3. reverse 颠倒列表内元素顺序

```sh
>>> a
['not', 'xiaoming', 18, 'good', 'i', 'am']

>>> a.reverse()
>>> a
['am', 'i', 'good', 18, 'xiaoming', 'not']
```



#### 4. sort 排序

```sh
排序时列表元素之间必须是相同数据类型，不可混搭，否则报错
>>> b =  [5,4,1,2]
>>> b.sort()
>>> b
[1, 2, 4, 5]
```



#### 5. 循环

```sh
b =  [5,4,1,2]
for l in b:
    print(l)

>>>            
5
4
1
2
```





### 四、元组

元组的元素不能修改，即元组相当于不可变的列表，用于记录多个固定不允许修改的值，单纯用于取

```sh
>>> tuple1 = (1, 'hhaha', 15000.00, 11, 22, 33) 
# 1、按索引取值(正向取+反向取)：只能取，不能改否则报错！  
>>> tuple1[0]
1
>>> tuple1[-2]
22
>>> tuple1[0] = 'hehe'  # 报错：TypeError:

# 2、切片(顾头不顾尾，步长)
>>> tuple1[0:6:2] 
(1, 15000.0, 22)

# 3、长度
>>> len(tuple1)  
6

# 4、成员运算 in 和 not in
>>> 'hhaha' in tuple1 
True
>>> 'hhaha' not in tuple1  
False 

# 5、循环
>>> for line in tuple1:
...     print(line)
1
hhaha
15000.0
11
22
33
```



### 五、字典

#### 1. 取值

##### 1.1 按keys取值

```sh
>>> dic
{'name': 'lijianli', 'age': 12, 'sex': 'man', 'hobby': ['movies', 'xiaoshuo', 'people']}

>>> dic['hobby']
['movies', 'xiaoshuo', 'people']

>>> dic['hobby'][1]
'xiaoshuo'
```

##### 1.2 dic.get取值

```sh
>>> dic= {'k1':'jason','k2':'Tony','k3':'JY'}
>>> dic.get('k1')
'jason'  # key存在，则获取key对应的value值

>>> res=dic.get('xxx') # key不存在，不会报错而是默认返回None
>>> print(res)
None  

>>> res=dic.get('xxx',666) # key不存在时，可以设置默认返回的值
>>> print(res)
666 
# ps:字典取值建议使用get方法
```



#### 2. 删除 pop popitem

<font color='red'>pop()删除指定的key对应的键值对,并返回值</font>

```sh
>>> dic= {'k1':'jason','k2':'Tony','k3':'JY'}
>>> v = dic.pop('k2')  # 删除指定的key对应的键值对,并返回值
>>> dic
{'k1': 'jason', 'kk2': 'JY'}
>>> v
'Tony'
```

<font color='red'>popitem()随机删除一组键值对,并将删除的键值放到元组内返回</font>

```sh
>>> dic= {'k1':'jason','k2':'Tony','k3':'JY'}
>>> item = dic.popitem()  # 随机删除一组键值对,并将删除的键值放到元组内返回
>>> dic
{'k3': 'JY', 'k2': 'Tony'}
>>> item
('k1', 'jason')
```



#### 3. 更新 update

```sh
# 用新字典更新旧字典，有则修改，无则添加
>>> dic= {'k1':'jason','k2':'Tony','k3':'JY'}
>>> dic.update({'k1':'JN','k4':'xxx'})
>>> dic
{'k1': 'JN', 'k3': 'JY', 'k2': 'Tony', 'k4': 'xxx'}
```

```sh
# 1.2 对于赋值操作，如果key原先不存在于字典，则会新增key:value
>>> dic['gender'] = 'male'  
>>> dic
{'name': 'tony', 'age': 18, 'hobbies': ['play game', 'basketball'],'gender':'male'}
# 1.3 对于赋值操作，如果key原先存在于字典，则会修改对应value的值
>>> dic['name'] = 'tony'
>>> dic
{'name': 'tony', 'age': 18, 'hobbies': ['play game', 'basketball']}
```



#### 4. 键keys()，值values()，键值对items()

```sh
>>> dic = {'age': 18, 'hobbies': ['play game', 'basketball'], 'name': 'xxx'}

# 获取字典所有的key
>>> dic.keys()  
dict_keys(['name', 'age', 'hobbies'])

# 获取字典所有的value
>>> dic.values()
dict_values(['xxx', 18, ['play game', 'basketball']])

# 获取字典所有的键值对
>>> dic.items()
dict_items([('name', 'xxx'), ('age', 18), ('hobbies', ['play game', 'basketball'])])
```



#### 5.  for循环

```sh
# 默认遍历的是字典的key
>>> for key in dic:
...     print(key)
... 
age
hobbies
name

# 只遍历key
>>> for key in dic.keys():
...     print(key)
... 
age
hobbies
name

# 只遍历value
>>> for key in dic.values():
...     print(key)
... 
18
['play game', 'basketball']
xxx

#遍历key与value
>>> for key in dic.items():
...     print(key)
... 
('age', 18)
('hobbies', ['play game', 'basketball'])
('name', 'xxx')
```



### 六、集合

<font color='red' >集合、list、tuple、dict一样都可以存放多个值，</font>但是集合主要用于：去重、关系运算集合去重复有局限性

```sh
# 1. 只能针对不可变类型 
# 2. 集合本身是无序的，去重之后无法保留原来的顺序              
```

```sh
# 针对不可变类型，并且保证顺序则需要我们自己写代码实现，例如
l=[
    {'name':'lili','age':18,'sex':'male'},
    {'name':'jack','age':73,'sex':'male'},
    {'name':'tom','age':20,'sex':'female'},
    {'name':'lili','age':18,'sex':'male'},
    {'name':'lili','age':18,'sex':'male'},
]

new_l=[]

for dic in l:
    if dic not in new_l:
        new_l.append(dic)

print(new_l)
# 结果：既去除了重复，又保证了顺序，而且是针对不可变类型的去重
[
    {'age': 18, 'sex': 'male', 'name': 'lili'}, 
    {'age': 73, 'sex': 'male', 'name': 'jack'}, 
    {'age': 20, 'sex': 'female', 'name': 'tom'}
]
```



### 七、字符编码

```sh
# 1、unicode格式------编码encode-------->其它编码格式
>>> x='上' # 在python3在'上'被存成unicode
>>> res=x.encode('utf-8')
>>> res,type(res) # unicode编码成了utf-8格式，而编码的结果为bytes类型，可以当作直接当作二进制去使用
(b'\xe4\xb8\x8a', <class 'bytes'>)

# 2、其它编码格式------解码decode-------->unicode格式
>>> res.decode('utf-8') 
'上'
```



### 八、文件操作

#### 1. 基础概念

文件使用：open()

```sh
1.1、强调：  t  和  b  不能单独使用，必须跟r/w/a连用

1.2、t文本（默认的模式）
   1. 读写以str(unicode)为单位
   2.文本文件
   3.必须制定encoding="utf-8"

1.3、b二进制/byte
```

2、控制文件读写操作模式

```sh
r(默认的)：只读
w：只写
a：只追加写
+：r+   a+   w+
```

3、基本流程

```sh
f = open('./a.txt','r',encoding='utf-8')
data = f.read()
f.close()
print(data)
```

4、资源回收与with上下文管理

```sh
with open('a.txt','r') as read_f,open('b.txt','w') as write_f:  
    data = read_f.read()
    write_f.write(data)
```



#### 2. 文件的操作模式

**r 模式**

```sh
# r只读模式: 在文件不存在时则报错,文件存在文件内指针直接跳到文件开头
 with open('a.txt',mode='r',encoding='utf-8') as f:
     res=f.read() # 会将文件的内容由硬盘全部读入内存，赋值给res
```

实现用户登陆

```sh
input_username = input("输入用户：")
input_password = input("输入密码：")

with open('a.txt',mode='rt',encoding='utf-8') as f:
    for line in f:
      username,password = line.strip().split(":")
      if username == input_username and password == input_password:
        print("login successful")
        break
    else:
      print("username  or password error")
```



**w 模式**

```sh
# w只写模式: 在文件不存在时会创建空文档,文件存在会清空文件,文件指针跑到文件开头
with open('b.txt',mode='w',encoding='utf-8') as f:
    f.write('你好\n')
    f.write('我好\n') 
    f.write('大家好\n')
    f.write('111\n222\n333\n')
#强调：
# 1 在文件不关闭的情况下,连续的写入，后写的内容一定跟在前写内容的后面
# 2 如果重新以w模式打开文件，则会清空文件内容
```

实现copy文件    

```sh
实现copy文件
src_file = input("输入源文件路径：")
des_file = input("输入目标文件路径：")

with open('{}'.format(src_file),mode='rt',encoding='utf-8') as f1,open('{}'.format(des_file),mode='wt') as f2:
     
       res =f1.read()
       f2.write(res)

print("copy   successful")
```



**a 模式**

```sh
3、a 模式
# a只追加写模式: 在文件不存在时会创建空文档,文件存在会将文件指针直接移动到文件末尾
 with open('c.txt',mode='a',encoding='utf-8') as f:
     f.write('44444\n')
     f.write('55555\n')
#强调 w 模式与 a 模式的异同：
# 1 相同点：在打开的文件不关闭的情况下，连续的写入，新写的内容总会跟在前写的内容之后
# 2 不同点：以 a 模式重新打开文件，不会清空原文件内容，会将文件指针直接移动到文件末尾，新写的内容永远写在最后
```

实现注册功能

```sh

实现注册功能:
name = input("enter name:")
passwd = input("enter  passwd:")
with open('e.txt',mode='at',encoding='utf-8') as f:
   f.write("{}:{}\n".format(name,passwd))
```



**+ 模式的使用(了解)**

\# r+ w+ a+ :可读可写 

#在平时工作中，我们只单纯使用r/w/a，要么只读，要么只写，一般不用可读可写的模式

**x 模式的使用(了解)**

\#只写模式，不存在创建，存在报错



#### 3.控制文件读写内容的模式

大前提: tb模式均不能单独使用,必须与r/w/a之一结合使用

**t（默认的）：文本模式**

```sh
1. 读写文件都是以字符串为单位的
2. 只能针对文本文件
3. 必须指定encoding参数
```

**b：二进制模式:**

```sh
1.读写文件都是以bytes/二进制为单位的
2. 可以针对所有文件
3. 一定不能指定encoding参数
```

**b 模式的使用**

while循环读取文件，以字节为单位

      ```sh
      with open('hashiq.jpg',mode='rb') as f:
        while  True:
          res = f.read(1024)
          if len(res) == 0:
            break
          print(len(res))
      ```

for循环读取文件,以行为单位

```sh
with open('hashiq.jpg',mode='rb') as f:
  for line in f:
    print(line)
```

​           

#### 4. 读相关操作

f.read()  

```sh
# 读取所有内容,执行完该操作后，文件指针会移动到文件末尾
```

f.readline()  

```sh
# 读取一行内容,光标移动到第二行首部
```

f.readlines()  

```sh
f.read()  # 读取所有内容,执行完该操作后，文件指针会移动到文件末尾
f.readline()  # 读取一行内容,光标移动到第二行首部
f.readlines()  # 读取每一行内容,存放于列表中
```

f.flush()  

```sh
# 立刻将文件内容从内存刷到硬盘      
```

​        

#### 5. 写相关操作

```sh
f.write('1111\n222\n')  # 针对文本模式的写,需要自己写换行符
f.write('1111\n222\n'.encode('utf-8'))  # 针对b模式的写,需要自己写换行符

f.writelines(['333\n','444\n'])  # 文件模式
f.writelines([bytes('333\n',encoding='utf-8'),'444\n'.encode('utf-8')]) #b模式
f.writelines(['333\n','444\n'])  # 文件模式，将列表中的数据写入到文件中
```



#### 6. 文件指针操作

```sh
#大前提:文件内指针的移动都是Bytes为单位的,唯一例外的是t模式下的read(n),n以字符为单位
with open('a.txt',mode='rt',encoding='utf-8') as f:
     data=f.read(3) # 读取3个字符


with open('a.txt',mode='rb') as f:
     data=f.read(3) # 读取3个Bytes


# 之前文件内指针的移动都是由读/写操作而被动触发的，若想读取文件某一特定位置的数据，
则则需要用f.seek方法主动控制文件内指针的移动，详细用法如下：

# f.seek(指针移动的字节数,模式控制): 
f.seek(3,0)     #

# 模式控制:
# 0: 默认的模式,该模式代表指针移动的字节数是以文件开头为参照的
# 1: 该模式代表指针移动的字节数是以当前所在的位置为参照的
# 2: 该模式代表指针移动的字节数是以文件末尾的位置为参照的
# 强调:其中0模式可以在t或者b模式使用,而1跟2模式只能在b模式下用
```

```sh
>>> cat  a.txt
123你好

with open('a.txt',mode='rt',encoding='utf-8') as f:
  f.seek(3,0)
  res1 = f.tell()
  print(res1)
  res = f.read()
  print(res)
```



#### 7. 文件的修改

```sh
with open('a.txt',mode='rt',encoding='utf-8') as f:
  data = f.read()
  
with open('a.txt',mode='wt',encoding='utf-8') as f:
  f.write(data.replace('你好','小明'))
```

​       



### 九、函数

#### 1 位置参数

位置即顺序，位置参数指的是按顺序定义的参数，需要从两个角度去看：

1. 在定义函数时，按照从左到右的顺序依次定义形参,称为位置形参，凡是按照这种形式定义的形参都必须被传值
2. 在调用函数时，按照从左到右的顺序依次定义实参，称为位置实参，凡是按照这种形式定义的实参会按照从左到右的顺序与形参一一对应

```sh
def register(name,age,sex): #定义位置形参：name，age，sex，三者都必须被传值
    print('Name:%s Age:%s Sex:%s' %(name,age,sex))
register('aa',12,'man')
```

​         

#### 2 关键字参数

在调用函数时，实参可以是key=value的形式，称为关键字参数，凡是按照这种形式定义的实参，可以完全不按照从左到右的顺序定义，但仍能为指定的形参赋值

需要注意在调用函数时，实参也可以是按位置或按关键字的混合使用，但必须保证关键字参数在位置参数后面，且不可以对一个形参重复赋值

```sh
def register(name,age,sex):
    print("%s %s %s" %(name,age,sex))
register(sex='male',name='lili',age=18)

>>> Name:lili Age:18 Sex:male        
```

  

#### 3 默认参数

在定义函数时，就已经为形参赋值，这类形参称之为默认参数，当函数有多个参数时，需要将值经常改变的参数定义成位置参数，而将值改变较少的参数定义成默认参数。例如编写一个注册学生信息的函数，如果大多数学生的性别都为男，那完全可以将形参sex定义成默认参数

          ```sh
          >>> def register(name,age,sex='male'): #默认sex的值为male
          ...     print('Name:%s Age:%s Sex:%s' %(name,age,sex))
          ```

需要注意：

1. 默认参数必须在位置参数之后
2. 默认参数的值仅在函数定义阶段被赋值一次



#### 4. 可变长度位置参数 (\*args)

如果在最后一个形参名前加*号,那么在调用函数时，*

*溢出的位置实参，都会被*接收，以元组的形式保存下来赋值给该形参

<font color='red'>实参1、2、3按位置为形参x、y、z赋值，多余的位置实参4、5、6、7都被\*接收，以元组的形式保存下来，赋值给args，即args=(4, 5, 6,7)</font>

```sh
>>> def foo(x,y,z=1,*args): #在最后一个形参名args前加*号
...     print(x)
...     print(y)
...     print(z)
...     print(args)
... 
>>> foo(1,2,3,4,5,6,7)  
1
2
3
(4, 5, 6, 7)
```

```sh
def my(*x):
    res = 0
    for item in x:
        res+=item
    return res

res=my(1,2,3,4)
print(res)
```



#### 5 可变长度关键字参数 (\**args)

如果在最后一个形参名前加号,那么在调用函数时，溢出的关键字参数，都会被接收，以字典的形式保存下来赋值给该形参

```sh
>>> def foo(x,**kwargs): #在最后一个参数kwargs前加**
...     print(x)        
...     print(kwargs)   
... 
>>> foo(y=2,x=1,z=3) #溢出的关键字实参y=2，z=3都被**接收，以字典的形式保存下来，赋值给kwargs
1
{'z': 3, 'y': 2}
```

```sh
# * 不光用在形参中，还可以用在实参中，先* ，然后打散成位置实参

def test(x,y,z):
    print(x,y,x)

test(*[1,2,3])
	
>>> test(*[1,2,3])
1 2 3


#形参和实参都带 *
>>> def my(x,y,*args):
	print(x,y,args)

>>> 

>>> my(1,2,*[4,5,6])
1 2 (4, 5, 6)
>>> 


#形参和实参都带 **
def func(x,y,**kwargs):
    print(x,y,kwargs)

func(**{'y':2,'x':1,'c':5,'d':7})

>>>  1 2 {'c': 5, 'd': 7}
```



#### 推导式

列表推导式是一种快速生成列表的方式。其形式是用方括号括起来的一段语句，如下例子所示：

```
lis = [x * x for x in range(1, 10)]

print(lis)
------------------------------------
结果：[1, 4, 9, 16, 25, 36, 49, 64, 81]
```

```
>>> [x * x for x in range(1, 11) if x % 2 == 0]
[4, 16, 36, 64, 100]
```



字典推导式

既然使用中括号[]可以编写列表推导式，那么使用大括号呢？你猜对了！使用大括号{}可以制造字典推导式！

注意`x: x**2`的写法，中间的冒号，表示左边的是key右边的是value。

```
>>> dic = {x: x**2 for x in (2, 4, 6)}
>>> dic
{2: 4, 4: 16, 6: 36}
>>> type(dic)
<class 'dict'>
```



集合推导式

大括号除了能用作字典推导式，还可以用作集合推导式，两者仅仅在细微处有差别。

```
>>> a = {x for x in 'abracadabra' if x not in 'abc'}
>>> a
{'d', 'r'}
>>> type(a)
<class 'set'>
```



元组推导式

报告老师，还有圆括号！是不是元组推导式？想法不错，但事实却没有。圆括号在Python中被用作生成器的语法了，很快我们就会讲到，没有元组推导式。



### 十、添加员工练习

```sh
"""
需求：员工管理系统
功能:
1.添加员工信息
2.删除员工信息
3.修改员工信息
4.查看单个员工信息
5.查看所有员工信息
6.退出

技术：函数、数据类型(字典列表)、循环、条件语句
"""
emps = []   # [{},{}]


def chocieFunc():
    """选择功能列表"""
    print("*" * 30)
    print("1.添加员工信息")
    print("2.删除员工信息")
    print("3.修改员工信息")
    print("4.查看单个员工信息")
    print("5.查看所有员工信息")
    print("6.退出")
    print("*" * 30)


def addEmp():
    """添加员工信息"""
    id = input("请输入要添加的员工编号：")
    name = input("请输入要添加的员工姓名：")
    gender = input("请输入要添加的员工性别：")
    age = input("请输入要添加的员工年龄：")
    emp = {"id": id, "name": name, "gender": gender, "age": age}
    emps.append(emp)
    print("添加OK！")


def delEmp():
    """删除员工信息"""
    id = input("请输入要删除的员工编号：")
    for emp in emps:
        if emp.get("id") == id:
            # 将emp删除,从emps
            emps.remove(emp)
            print("删除OK！")
            break
    else:
        print("请输入正确的员工编号")


def updateEmp():
    """修改员工信息"""
    id = input("请输入要修改的员工编号：")
    for emp in emps:
        if emp["id"] == id:
            # 特别注意
            emp["name"] = input("请输入要修改后的员工姓名：")
            emp["gender"] = input("请输入要修改后的员工性别：")
            emp["age"] = input("请输入要修改后的员工年龄：")
            # emp = {"id": id, "name": name, "gender": gender, "age": age}
            # 先删除原有的emp,在追加新的emp【不推荐】
            print("修改成功！！！")
            break
    else:
        print("查无此人！！！")


def getEmpById():
    """查看单个员工信息"""
    id = input("请输入要查询的员工编号：")
    for emp in emps:
        if emp["id"] == id:
            print("编号\t姓名\t性别\t年龄")
            print(f"{emp['id']}\t{emp['name']}\t{emp['gender']}\t{emp['age']}")
            break
    else:
        print("查无此人！！！")


def getAllEmps():
    """查看所有员工信息"""
    print("编号\t姓名\t性别\t年龄")
    for emp in emps:
        print(f"{emp['id']}\t{emp['name']}\t{emp['gender']}\t{emp['age']}")
    else:
        print(f"共查询到{len(emps)}条数据")


print("******欢迎使用员工管理系统******")
while True:
    chocieFunc()
    num = int(input("请输入指令:"))
    if num == 1:
        addEmp()
    elif num == 2:
        delEmp()
    elif num == 3:
        updateEmp()
    elif num == 4:
        getEmpById()
    elif num == 5:
        getAllEmps()
    elif num == 6:
        print("欢迎下次再来！！！")
        break
    else:
        print("请输入正确的指令")
```





# 模块

#### 异常

**1、try----except**

```sh
while True:
    try:
        x = int(input("请输入一个数字: "))
        break
    except ValueError:
        print("您输入的不是数字，请再次尝试输入！")
```

**2、try----except----else**

```sh
for arg in sys.argv[1:]:
    try:
        f = open(arg, 'r')
    except IOError:
        print('cannot open', arg)
    else:
        print(arg, 'has', len(f.readlines()), 'lines')
        f.close()
```

**3、try----finally**

```sh
try:
    runoob()
except AssertionError as error:
    print(error)
else:
    try:
        with open('file.log') as file:
            read_data = file.read()
    except FileNotFoundError as fnf_error:
        print(fnf_error)
finally:
    print('这句话，无论异常是否发生都会执行。')
```

**4、万能异常**

```sh
s1 = 'hello'==
try:
    int(s1)

except Exception as e:
    print('错误')
```

**5、异常种类**

```sh
 BaseException                     # 所有异常的父类
    - SystemExit                     # 由sys.exit()抛出的异常
    - KeyBoardInterrupt              # 通常由ctrl+c或者Delete抛出的异常
    - GeneratorExit                  # 当生成器被关闭时抛出的异常
    - Exception                      # 
        - StopIteration              # 迭代结束异常
        - StopAsyncIteration         # 由异步迭代的`__anext__()`抛出的异常
        - ArithmeticError            # 各种算数错误引起的异常
            - FloatingPointError     # 浮点数操作错误
            - OverflowError          # 结果超出范围
            - ZeroDivisionError      # ０为除数异常
    - AssertionError                 # assert错误异常
    - AttributeError                 # 属性引用异常
    - BufferError                    # 缓存错误
    - EOFError                       # 读不到数据
    - ImportError                    # import错误
        - ModuleNotFoundError        # 找不多模块
    - LookupError                    # 由索引和key值引起的异常
        - IndexError                 # 索引错误
        - KeyError                   # 字典key值错误
    - MemortError                    # 内存溢出异常
    - NameError                      # 本地和全局找不到变量名
        - UnboundLocalError          # 局部变量没有赋值
    - OSError                        # system错误
        - BlockingIOError            # 调用阻塞异常错误
        - ChildProcessError          # 子进程
        - ConnectionError            # 连接
            - BrokenPipeError        # 管道读写异常
            - ConnectionAbortedError # 连接失败
            - ConnectionRefusedError # 连接拒绝
            - ConnectionResetError   # 连接重置
        - FileExistsError            # 创建文件和文件夹错误
        - FileNotFoundError          # 文件未找到
        - InterruptedError           # 中断错误
        - IsADirectoryError          # 文件操作用在文件夹上
        - NotADirectoryError         # 不是文件夹
        - PermissionError            # 权限
        - ProcessLookupError         # 进程不存在
        - TimeoutError               # 超时
    - ReferenceError                 # 引用异常
    - RuntimeError                   # 
        - NotImplementedError        # 运行抽象方法
        - RecursionError             # 超出最大递归深度
    - SyntaxError                    # 语法错误
        - IndentationError           # 缩进错误
            - TabError               # tab错误
    - SystemError                    # 解释器中断
    - TypeError                      # 类型错误
    - ValueError                     # 赋值错误
        - UnicodeError               # 
            - UnicodeEncodeError     # unicode编码错误
            - UnicodeDecodeError     # unicode解码错误
            - UnicodeTranslateError  # unicode转换错误
    - Warning                        # 
        - DeprecationWarning         # 操作不赞成警告
        - PendingDeprecationWarning  # 表明此操作将来会被弃用
        - UserWarning                # 用于用户生成警告
        - SyntaxWarning              # 语法可疑警告
        - RuntimeWarning             # 运行警告
        - FutureWarning              # 将会改变警告
        - ImportWarning              # 导入警告
        - UnicodeWarning             # unicode相关警告
        - BytesWarning               # 字节相关警告
        - ResourceWarning            # 资源使用情况警告
```







#### 图形验证码

```python
def get_code(request):
    # 步骤一 文件读取
    # with open(r'C:\Users\Administrator\PycharmProjects\djangoProject1\avatar\default.jpg','rb') as f:
    #    data = f.read()
    # return HttpResponse(data)

    # 步骤二  生成图片
    # image_obj = Image.new('RGB',(430,34),get_random())
    # #保存图片
    # with open('xxx.png','wb') as f:
    #     image_obj.save(f,'png')
    # with  open('xxx.png','rb') as f:
    #     data = f.read()
    # return HttpResponse(data)

    # 步骤三  内存存取图片
    # image_obj = Image.new('RGB',(500,34),get_random())
    # io_obj = BytesIO()
    # image_obj.save(io_obj,'png')
    # return HttpResponse(io_obj.getvalue())

    # 生成文字
    img_obj = Image.new('RGB', (500, 34), get_random())
    img_draw = ImageDraw.Draw(img_obj)  #产生画笔对象
    img_font = ImageFont.truetype('static/abc.ttf', 30) #字体样式 大小

    # 随机验证码
    code = ''
    for i in range(5):
        random_upper = chr(random.randint(65, 90))
        random_lower = chr(random.randint(97, 122))
        random_int = str(random.randint(0, 9))
        tmp = random.choice([random_int, random_upper, random_lower])
        # 为什么一个个生成好再写  可以控制字体间隙
        img_draw.text((i*60, 0), tmp, get_random(), img_font)
        code += tmp
    print(code)
    request.session['code'] = code
    io_obj = BytesIO()
    img_obj.save(io_obj, 'png')
    return HttpResponse(io_obj.getvalue())
```





#### 正则表达式

```sh
#匹配邮箱
email_re = re.match(r'^[0-9a-zA-Z_]{0,19}@[0-9a-zA-Z]{1,13}\.[0-9a-zA-Z]{1,3}$', email)
#匹配手机号
ret = re.match(r"^1[35789]\d{9}$", tel)
```

 字符组

| `正则`         | `待匹配字符` | `匹配结果` | `说明`                                                       |
| -------------- | ------------ | ---------- | ------------------------------------------------------------ |
| `[0123456789]` | `8`          | `True`     | `在一个字符组里枚举合法的所有字符，字符组里的任意一个字符和"待匹配字符"相同都视为可以匹配` |
| `[0123456789]` | `a`          | `False`    | `由于字符组中没有"a"字符，所以不能匹配`                      |
| `[0-9]`        | `7`          | `True`     | `也可以用-表示范围,[0-9]就和[0123456789]是一个意思`          |
| `[a-z]`        | `s`          | `True`     | `同样的如果要匹配所有的小写字母，直接用[a-z]就可以表示`      |
| `[A-Z]`        | `B`          | `True`     | `[A-Z]就表示所有的大写字母`                                  |
| `[0-9a-fA-F]`  | `e`          | `True`     | `可以匹配数字，大小写形式的a～f，用来验证十六进制字符`       |

 2、字符

| `元字符` | `匹配内容`                         |
| -------- | ---------------------------------- |
| .        | 匹配除换行符以外的任意字符         |
| \w       | 匹配字母或数字或下划线             |
| \s       | 匹配任意的空白符                   |
| \d       | 匹配数字                           |
| \n       | 匹配一个换行符                     |
| \t       | 匹配一个制表符                     |
| \b       | 匹配一个单词的结尾                 |
| ^        | 匹配字符串的开始                   |
| $        | 匹配字符串的结尾                   |
| \W       | `匹配非字母或数字或下划线`         |
| \D       | `匹配非数字`                       |
| \S       | `匹配非空白符`                     |
| a\|b     | `匹配字符a或字符b`                 |
| ()       | `匹配括号内的表达式，也表示一个组` |
| [...]    | `匹配字符组中的字符`               |
| [^...]   | `匹配除了字符组中字符的所有字符`   |

3、量词

| `量词` | `用法说明`       |
| ------ | ---------------- |
| *      | 重复零次或更多次 |
| +      | 重复一次或更多次 |
| ?      | 重复零次或一次   |
| {n}    | 重复n次          |
| {n,}   | 重复n次或更多次  |
| {n,m}  | 重复n到m次       |

```sh
# ===========================re模块提供的方法介绍===========================
import re
#1
print(re.findall('e','alex make love') )   #['e', 'e', 'e'],返回所有满足匹配条件的结果,放在列表里

#2
print(re.search('e','alex make love').group()) #e,只到找到第一个匹配然后返回一个包含匹配信息的对象,
该对象可以通过调用group()方法得到匹配的字符串,如果字符串没有匹配，则返回None。

#3
print(re.match('e','alex make love'))    #None,同search,不过在字符串开始处进行匹配,完全可以用search+^代替match

#4
print(re.split('[ab]','abcd'))     #['', '', 'cd']，先按'a'分割得到''和'bcd',再对''和'bcd'分别按'b'分割

#5
print('===>',re.sub('a','A','alex make love')) #===> Alex mAke love，不指定n，默认替换所有
print('===>',re.sub('a','A','alex make love',1)) #===> Alex make love
print('===>',re.sub('a','A','alex make love',2)) #===> Alex mAke love
print('===>',re.sub('^(\w+)(.*?\s)(\w+)(.*?\s)(\w+)(.*?)$',r'\5\2\3\4\1','alex make love')) #===> love make alex

print('===>',re.subn('a','A','alex make love')) #===> ('Alex mAke love', 2),结果带有总共替换的个数


#6
obj=re.compile('\d{2}')

print(obj.search('abc123eeee').group()) #12
print(obj.findall('abc123eeee')) #['12'],重用了obj
```





#### pymysql

sql注入

```sh
import pymysql

conn = pymysql.connect(
    host = "127.0.0.1",
    port = 3306,
    user = "root",
    password = "123",
    db = "test_7_17"
    # autocommit = False  # 如果改成True 就表示开启自动提交,不常用,pymysql中默认开启事务,所以我们必须在每次执行完成后,commit提交下
)
c = conn.cursor(pymysql.cursors.DictCursor)

name = input("name>>>").strip()
pwd = input("pwd>>>").strip()
# 不能把变量名直接放到sql执行语句中,防止sql攻击
sql = "select * from user where name = %s and pwd = %s"

count = c.execute(sql,(name,pwd))

if count:
    print("登陆成功")
else:
    print("登陆失败")
print(c.fetchall())
c.scroll(-2,mode="relative")

print(c.fetchone())
c.scroll(0,mode="absolute")
print(c.fetchmany(2))
```

**增、删、改：conn.commit()**

```python
import pymysql
#链接
conn=pymysql.connect(host='localhost',user='root',password='123',database='egon')
#游标
cursor=conn.cursor()

#part1
# sql='insert into userinfo(name,password) values(%s,%s);'
# res=cursor.execute(sql,("root","123456")) #执行sql语句，返回sql影响成功的行数
# print(res)

#part2
sql='insert into userinfo(name,password) values(%s,%s);'
res=cursor.executemany(sql,[("root","123456"),("lhf","12356"),("eee","156")]) #执行sql语句，返回sql影响成功的行数
print(res)

conn.commit() #提交后才发现表中插入记录成功
cursor.close()
conn.close()
```

**查：fetchone，fetchmany，fetchall**

```python
import pymysql
#建立与数据库的连接
conn=pymysql.connect(host='localhost',user='root',password='',database='db2')

#创建游标
cursor=conn.cursor()

#执行sql语句
sql='select * from user;'
rows=cursor.execute(sql)            #返回的是表中所有记录的条数
cursor.scroll(3,mode='absolute') # 相对绝对位置移动，第一个参数是相对绝对位置移动的记录条个数
# cursor.scroll(1,mode='relative') # 相对当前位置移动，第一个参数是相对当前位置移动的记录条个数

#通过fetchone、fetchmany、fetchall拿到查询结果
res1=cursor.fetchone()              #以元组的形式，返回查询记录的结果，默认是从第一条记录开始查询
# res2=cursor.fetchone()            #会接着上一次的查询记录结果继续往下查询
# res3=cursor.fetchone()
# res4=cursor.fetchmany(2)           #查询两条记录会以元组套小元组的形式进行展示
# res5=cursor.fetchall()

#打印查询的最终结果到终端
print(res1)
# print(res2)
# print(res3)
# print(res4)
# print(res5)                         #会元组套小元组的形式将表中的左右记录头查询出来展示在终端
print('%s行数据'%rows)
```

fetch获取的数据默认是元组，如果想要字典类型：

```
import pymysql
#链接
conn=pymysql.connect(host='localhost',user='root',password='',database='db2')
#游标
cursor=conn.cursor(cursor=pymysql.cursors.DictCursor)#在此处设置
#执行sql语句
sql='select * from user;'
rows=cursor.execute(sql)
res1=cursor.fetchone()          #查询的结果就是一个字典的形式，字典的key就是对应的字段名，value就是字段名对应的记录内容
# res1=cursor.fetchall()        #查询多条或所有结果是一个列表中套着一个一个字典
print(res1)
```





#### OS

os模块提供了一些操作系统相关的变量，可以在跨平台的时候提供支持，便于编写移植性高，可用性好的代码。所以在涉及操作系统相关的操作时，请尽量使用本模块提供的方法，而不要使用当前平台特定的用法或格式，否则一旦移植到其他平台，可能会造成难以解决的困扰。

| 方法和变量 | 用途                                                         |
| ---------- | ------------------------------------------------------------ |
| os.name    | 查看当前操作系统的名称。windows平台下返回‘nt’，Linux则返回‘posix’。 |
| os.environ | 获取系统环境变量                                             |
| os.sep     | 当前平台的路径分隔符。在windows下，为‘\’，在POSIX系统中，为‘/’。 |
| os.altsep  | 可替代的路径分隔符，在Windows中为‘/’。                       |
| os.extsep  | 文件名和文件扩展名之间分隔的符号，在Windows下为‘.’。         |
| os.pathsep | PATH环境变量中的分隔符，在POSIX系统中为‘:’，在Windows中为‘;’。 |
| os.linesep | 行结束符。在不同的系统中行尾的结束符是不同的，例如在Windows下为‘\r\n’。 |
| os.devnull | 在不同的系统上null设备的路径，在Windows下为‘nul’，在POSIX下为‘/dev/null’。 |
| os.defpath | 当使用exec函数族的时候，如果没有指定PATH环境变量，则默认会查找os.defpath中的值作为子进程PATH的值。 |

使用范例：

```
>>> import os
>>> os.name
'nt'
>>> os.environ
environ({'ALLUSERSPROFILE': 'C:\\ProgramData', 'APPDATA': 'C:\\Users\\Administrator\\AppData\\Roaming', 'ASL.LOG': 'Destination=file', ......
>>> os.sep
'\\'
>>> os.altsep
'/'
>>> os.extsep
'.'
>>> os.pathsep
';'
>>> os.linesep
'\r\n'
>>> os.devnull
'nul'
>>> os.defpath
'.;C:\\bin'
```

os模块中包含了一系列文件操作相关的函数，其中有一部分是Linux平台专用方法。Linux是用C写的，底层的`libc`库和系统调用的接口都是`C API`，Python的os模块中包括了对这些接口的Python实现，通过Python的os模块，可以调用Linux系统的一些底层功能，进行系统编程。关于Linux的相关方法，内容较为复杂，可根据需要自行查阅官方文档，这里只介绍一些常用的，各平台通用的方法。

| 方法和变量                          | 用途                                                         |
| ----------------------------------- | ------------------------------------------------------------ |
| os.getcwd()                         | 获取当前工作目录，即当前python脚本工作的目录路径             |
| os.chdir("dirname")                 | 改变当前脚本工作目录；相当于shell下cd                        |
| os.curdir                           | 返回当前目录: ('.')                                          |
| os.pardir                           | 获取当前目录的父目录字符串名：('..')                         |
| os.makedirs('dir1/dir2')            | 可生成多层递归目录                                           |
| os.removedirs(‘dirname1’)           | 递归删除空目录（要小心）                                     |
| os.mkdir('dirname')                 | 生成单级目录                                                 |
| os.rmdir('dirname')                 | 删除单级空目录，若目录不为空则无法删除并报错                 |
| os.listdir('dirname')               | 列出指定目录下的所有文件和子目录，包括隐藏文件               |
| os.remove('filename')               | 删除一个文件                                                 |
| os.rename("oldname","new")          | 重命名文件/目录                                              |
| os.stat('path/filename')            | 获取文件/目录信息                                            |
| os.path.abspath(path)               | 返回path规范化的绝对路径                                     |
| os.path.split(path)                 | 将path分割成目录和文件名二元组返回                           |
| os.path.dirname(path)               | 返回path的目录。其实就是`os.path.split(path)`的第一个元素    |
| os.path.basename(path)              | 返回path最后的文件名。如果path以`／`或`\`结尾，那么就会返回空值。 |
| os.path.exists(path或者file)        | 如果path存在，返回True；如果path不存在，返回False            |
| os.path.isabs(path)                 | 如果path是绝对路径，返回True                                 |
| os.path.isfile(path)                | 如果path是一个存在的文件，返回True。否则返回False            |
| os.path.isdir(path)                 | 如果path是一个存在的目录，则返回True。否则返回False          |
| os.path.join(path1[, path2[, ...]]) | 将多个路径组合后返回，第一个绝对路径之前的参数将被忽略       |
| os.path.getatime(path)              | 返回path所指向的文件或者目录的最后存取时间                   |
| os.path.getmtime(path)              | 返回path所指向的文件或者目录的最后修改时间                   |
| os.path.getsize(filename)           | 返回文件包含的字符数量                                       |

在Python中，使用windows的文件路径时一定要小心，比如你要引用d盘下的1.txt文件，那么路径要以字符串的形式写成`'d:\\1.txt'`或者`r'd:\1.txt`。前面的方式是使用windwos的双斜杠作为路径分隔符，后者是使用`原生字符串`的形式，以r开始的字符串都被认为是原始字符串，表示字符串里所有的特殊符号都以本色出演，不进行转义，此时可以使用普通windows下的路径表示方式。这两种方法使用哪种都可以，但不可混用。

下面是一些使用的例子，建议大家都跟着做一遍(其中有一些是错误示范，让你更清楚它的用法)。

```
>>> os.getcwd()
'C:\\Python36'
>>> os.chdir("d:")
>>> os.getcwd()
'D:\\'
>>> os.curdir
'.'
>>> os.pardir
'..'
>>> os.makedirs("1\\2")
>>> os.removedirs("1\\2")
>>> os.listdir()
['$360Section', '$RECYCLE.BIN', '1.txt', 'MobileFile', 'pymysql_test.py', 'System Volume Information', '用户目录']
>>> os.mkdir("1")
>>> os.listdir()
['$360Section', '$RECYCLE.BIN', '1', '1.txt', 'MobileFile', 'pymysql_test.py', 'System Volume Information', '用户目录']
>>> os.rmdir("1")
>>> os.rename('1.txt','2.txt')
>>> os.listdir()
['$360Section', '$RECYCLE.BIN', '2.txt', 'MobileFile', 'pymysql_test.py', 'System Volume Information', '用户目录']
>>> os.remove('1.txt')
Traceback (most recent call last):
  File "<pyshell#22>", line 1, in <module>
    os.remove('1.txt')
FileNotFoundError: [WinError 2] 系统找不到指定的文件。: '1.txt'
>>> os.remove('2.txt')
>>> os.stat()
Traceback (most recent call last):
  File "<pyshell#24>", line 1, in <module>
    os.stat()
TypeError: Required argument 'path' (pos 1) not found
>>> os.stat(os.getcwd())
os.stat_result(st_mode=16895, st_ino=1407374883553285, st_dev=2431137650, st_nlink=1, st_uid=0, st_gid=0, st_size=32768, st_atime=1505824872, st_mtime=1505824872, st_ctime=1445187376)
```

更多的操作：

```
>>> import os
>>> os.chdir("d:")
>>> os.getcwd()
'D:\\'
>>> os.mkdir('test')
>>> os.listdir()
['$360Section', '$RECYCLE.BIN', 'MobileFile', 'pymysql_test.py', 'System Volume Information', 'test', '用户目录']
>>> os.chdir('test')
>>> os.getcwd()
'D:\\test'
>>> os.path.abspath(os.getcwd())
'D:\\test'
>>> os.path.split(os.getcwd())
('D:\\', 'test')
>>> cp = os.getcwd()
>>> os.path.dirname(cp)
'D:\\'
>>> os.path.basename(cp)
'test'
>>> os.path.exists(cp)
True
>>> os.path.exists("d:\\123\123")
False
>>> os.path.isabs(cp)
True
>>> os.path.isabs("11\\1.py")
False
>>> os.path.isfile(cp)
False
>>> os.path.isfile("d:\\1.txt")
False
>>> os.path.isdir(cp)
True
>>> os.path.join(cp, "test.py")
'D:\\test\\test.py'
>>> os.path.getatime(cp)
1505825113.4970243
>>> os.path.getmtime(cp)
1505825113.4970243
>>> os.path.getsize(cp)
0
```





#### 腾讯云短信

```sh
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="/static/bootstrap.css">
    <script src="/static/jquery-3.5.1.js"></script>
    <script src="/static/bootstrap.js"></script>
</head>
<body>

<div class="container-fluid">
    <div class="row">
        <div class="col-md-8 col-md-offset-2" style="margin-top: 100px">
            <h1 class="text-center">小 李 博 客 注 册</h1>
            <div class="form-group">
                <label for="username">用户名</label>
                <input type="text" name="username" id="username" class="form-control">
            </div>
            <div class="form-group">
                <label for="password">密码</label>
                <input type="password" name="password" id="password" class="form-control">
            </div>

            <div class="form-group">
                <label for="confirm_password">确认密码</label>
                <input type="password" name="confirm_password" id="confirm_password" class="form-control">
            </div>

            <div class="form-group">
                <label for="phone">手机号</label>
                <input type="text" name="phone" id="phone" class="form-control">
            </div>

            <div class="form-group">
                <label for="">手机验证码</label>
                <div class="row">
                    <div class="col-md-6">
                        <input type="text" name="phone_code" id="phone_code" class="form-control">
                    </div>
                    <div class="col-md-6" >
                        <input type="button" class="btn btn-default form-control" value="点击获取验证码" id="btnSms">
                    </div>

                </div>
            </div>

            <input type="button" class="btn btn-success form-control" value="注册" id="id_register">
            <span style="color: red" id="error"></span>
        </div>
    </div>
</div>

<script>
    $("#btnSms").click(function (){
        $.ajax({
            url: '/send_sms/',
            type: 'post',
            data: {
                'phone':$('#phone').val(),
                'csrfmiddlewaretoken': '{{ csrf_token }}'
            },
            success: function (args){
                if(args.code == 1000){
                    sendSmsRemind();

                }else{
                    $('#error').text(args.msg)
                }
            }
        })

    })

    function sendSmsRemind(){
        var $smsBtn = $('#btnSms');
        $smsBtn.prop('disabled',true);
        var time = 60;
        var remind = setInterval(function (){
            $smsBtn.val(time + '秒发送');
            time = time -1;
            if (time<1){
                clearInterval(remind);
                $smsBtn.val('点击获取验证码').prop('disabled',false);
            }
        },1000)
    }

    $("#id_register").click(function (){
        $.ajax({
            url: '',
            type: 'post',
            data:{
                'username': $('#username').val(),
                'password': $('#password').val(),
                'confirm_password': $('#confirm_password').val(),
                'phone': $('#phone').val(),
                'phone_code': $('#phone_code').val(),
                'csrfmiddlewaretoken': '{{ csrf_token }}'
            },
            success: function (args){
                if(args.code == 1000){
                    window.location.href = '/login/'
                }else{
                    $('#error').text(args.msg)
                }
            }
        })
    })
</script>

</body>
</html>
```

```sh
from django.test import TestCase

# Create your tests here.
# -*- coding:utf-8 -*-
import ssl
# ssl._create_default_https_context = ssl._create_unverified_context
from qcloudsms_py import SmsMultiSender, SmsSingleSender
from qcloudsms_py.httpclient import HTTPError


def send_sms_single(phone_num, template_id, template_param_list):
    """
    单条发送短信
    :param phone_num: 手机号
    :param template_id: 腾讯云短信模板ID
    :param template_param_list: 短信模板所需参数列表，例如:【验证码：{1}，描述：{2}】，则传递参数 [888,666]按顺序去格式化模板
    :return:
    """
    appid = 14006075  # 自己应用ID
    appkey = ""  # 自己应用Key
    sms_sign = ""  # 自己腾讯云创建签名时填写的签名内容（使用公众号的话这个值一般是公众号全称或简称）
    sender = SmsSingleSender(appid, appkey)
    try:
        response = sender.send_with_param(86, phone_num, template_id, template_param_list, sign=sms_sign)
    except HTTPError as e:
        response = {'result': 1000, 'errmsg': "网络异常发送失败"}
    return response


# if __name__ == '__main__':
#     result1 = send_sms_single("13582288129", 1215032, [666, ])
#     print(result1)

```





#### Excel数据导入mysql

```sh
[root@localhost ~]# cat a.py 
import pandas as pd  #先装个pandas ,pip install pandas
import pymysql

#读入数据库
filename="/root/test.xlsx"   #本地需要导入数据库的文件
data=pd.read_excel(filename)

# 建立数据库连接
db = pymysql.connect(host="127.0.0.1", port=3306, user="root", password="123456", db="test", charset="utf8")
cursor = db.cursor()

# 判断数据表是否存在
#try:
#    cursor.execute(
#        'create table student(id int auto_increment primary key,ip varchar(100),name varchar(30),password varchar(20))'
#    )
#except Exception as e:
#    raise e

query = 'insert into student(ip,name,password) values(%s,%s,%s)'

for i in range(0,len(data)):
   ip = data.iloc[i,0]
   name = data.iloc[i,1]
   password = data.iloc[i,2]
   values = (str(ip), str(name), str(password))
   cursor.execute(query,values)
cursor.close()
db.commit()
print("数据成功导入")
db.close()
```









# DJANGO

### 模板语法配置

```sh
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [os.path.join(BASE_DIR, "template")],  # template文件夹位置
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```



### 静态文件配置

```sh
STATIC_URL = '/static/'  # HTML中使用的静态文件夹前缀
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, "static"),  # 静态文件存放位置
]
```

static多目录访问,在static下找不到，去static1下找

```Python
#static多目录访问,在static下找不到，去static1下找
STATIC_URL = '/static/'  #令牌前缀  如果这个换了 对应的 HTML页面也要换
STATICFILES_DIRS = [
    os.path.join(BASE_DIR,'static'),
    os.path.join(BASE_DIR,'static1'),
]
```

static动态文件配置

```sh
STATIC_URL = '/static/'

#HTML页面 静态文件动态解析
{% load static %}
<link rel="stylesheet" href="{% static 'bootstrap.min.css' %}">
<script src="{% static 'bootstrap.min.js' %}"></script>
```



### 模板继承

```sh
#主home页面，用来包含侧边栏功能
{% include "cebianlan.html" %}

#导航栏继承home页面
{% extends "home.html" %}
{% block content %}
{% endblock %}

#home页面中
{% block content %}
{% endblock %}
```



### test文件

```sh
from django.test import TestCase
import os
import sys
if __name__ == "__main__":
    os.environ.setdefault("DJANGO_SETTINGS_MODULE", "test1.settings")
    import  django
    django.setup()
    from app02 import  models
    a = models.User.objects.all()
    print(a)
```



### request请求

```sh
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    {#    <link rel="stylesheet" href="/static/bootstrap.min.css">#}
    {#    <script src="/static/bootstrap.min.js"></script>#}
    {% load static %}
    <link rel="stylesheet" href="{% static 'bootstrap.min.css' %}">
    <script src="{% static 'bootstrap.min.js' %}"></script>
</head>
<body>
<h1 class="text-center">登录</h1>
<div class="container">
    <div class="row">
        <div class="col-md-8 col-md-offset-2">
            <form action="/login/" METHOD="POST">
                <p>username:<input type="text" name="username" class="form-control"></p>
                <p>password:<input type="password" name="password" class="form-control"></p>
                <input type="submit" class="btn btn-success btn-block">
            </form>
        </div>
    </div>
</div>
</body>
</html>
```

request.POST.get  获取列表最后一个元素
request.POST.getlist  获取整个列表

```python
from django.shortcuts import render, HttpResponse, redirect
def login(request):
    if request.method == "POST":
        print(request.POST)
        username = request.POST.get('username')
        password = request.POST.getlist('password')
        print(username,password)
        return  HttpResponse("收到")
    return render(request, 'login.html')
```



### 链接mysql

```sh
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'bbs',
        'USER': 'root',
        'PASSWORD': '123456',
        'HOST': '10.0.0.9',
        'PORT': 3306,
        'CHARSET': 'utf8'
    }
}
```

在init.py中

```sh
import pymysql
pymysql.install_as_MySQLdb()
```



### auth模块

登录功能

```html
<form action="" METHOD="POST">
    {% csrf_token %}
    <p>username:<input type="text" name="username" class="form-control"></p>
    <p>password:<input type="password" name="password" class="form-control"></p>
    <input type="submit">
</form>
```

```python
from django.shortcuts import render,HttpResponse
from django.contrib import  auth

def login(request):
    if request.method == 'POST':
       username = request.POST['username']
       password = request.POST['password']
       user_obj = auth.authenticate(username=username, password=password)
       if user_obj:
           return  HttpResponse("success")
       else:
           return HttpResponse("faild")
    return render(request,'login.html')
```

判断请求是否通过了认证。

```
def my_view(request):
  if not request.user.is_authenticated():
    return redirect('%s?next=%s' % (settings.LOGIN_URL, request.path))
```

登录装饰器

```python
settings配置文件中
LOGIN_URL = '/login/'  # 这里配置成你项目登录页面的路由
```

```sh
from django.contrib.auth.decorators import login_required
@login_required()
```

创建新用户

```
from django.contrib.auth.models import User
user = User.objects.create_user（username='用户名',password='密码',email='邮箱',...）
```

创建超级用户

```
from django.contrib.auth.models import User
user = User.objects.create_superuser（username='用户名',password='密码',email='邮箱',...）
```

检查密码

```
ok = user.check_password('密码')
```

注销功能

```python
@login_required()
def logout(request):
    auth.logout(request)  #类似request.session.flush
    return HttpResponse('退出')
```

修改密码

```sh
from django.contrib.auth.models import User
u = User.objects.get(username='your_name')
u.set_password('new_password')
u.save()
```

更改密码

```python
@login_required
def set_password(request):
    user = request.user
    err_msg = ''
    if request.method == 'POST':
        old_password = request.POST.get('old_password', '')
        new_password = request.POST.get('new_password', '')
        repeat_password = request.POST.get('repeat_password', '')
        # 检查旧密码是否正确
        if user.check_password(old_password):
            if not new_password:
                err_msg = '新密码不能为空'
            elif new_password != repeat_password:
                err_msg = '两次密码不一致'
            else:
                user.set_password(new_password)
                user.save()
                return redirect("/login/")
        else:
            err_msg = '原密码输入错误'
    content = {
        'err_msg': err_msg,
    }
    return render(request, 'set_password.html', content)
```

扩展author表

```sh
from django.contrib.auth.models import AbstractUser
class UserInfo(AbstractUser):
    """
    用户信息表
    """
    nid = models.AutoField(primary_key=True)
    phone = models.CharField(max_length=11, null=True, unique=True)
    
    def __str__(self):
        return self.username
```

按上面的方式扩展了内置的auth_user表之后，一定要在settings.py中告诉Django，我现在使用我新定义的UserInfo表来做用户认证。

```python
# 引用Django自带的User表，继承使用时需要设置
AUTH_USER_MODEL = "app名.UserInfo"
```



### json response

```python
import json
def user_json(request):
    usr_dict = {"name":"zs","password":"11我是你爹23","hbby":"girl"}
    j_d = json.dumps(usr_dict,ensure_ascii=False)
    return  HttpResponse(j_d)
```

```python
import json
from django.http import JsonResponse
def user_json(request):
    usr_dict = {"name":"zs","password":"11我是你爹23","hbby":"girl"}
    # j_d = json.dumps(usr_dict,ensure_ascii=False)
    # return  HttpResponse(j_d)
    return  JsonResponse(usr_dict,json_dumps_params={'ensure_ascii':False})
```

```python
from django.http import JsonResponse
def user_json(request):
    l = ['1','2']
    return  JsonResponse(l,safe=False)
```



### form上传文件

```sh
<body>
<form action="" method="POST" enctype="multipart/form-data">
    <p>username:<input type="text" name="username"></p>
    <p>file:<input type="file" name="file"></p>
    <input type="submit">
</form>
</body>
```

```sh
def ab_file(request):
    if request.method == "POST":
        file_obj = request.FILES.get('file')
        with open(file_obj.name,'wb') as f:
            for line in file_obj.chunks():
                f.write(line)
    return  render(request,'form.html')
```



### 登录功能实例

urls.py

```sh
from django.conf.urls import url
from django.contrib import admin
from app01 import views
urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'^login/', views.login),
    url(r'^register/', views.register),
    url(r'^logout/', views.logout),
    url(r'^home/', views.home),
    url(r'set_password/', views.set_password),
    url(r'get_code/', views.get_code),
]
```

views.py

```python
from io import BytesIO
import random

from django.http import JsonResponse
from django.shortcuts import render, HttpResponse, redirect
from django.contrib.auth.models import User
from django.contrib import auth
from django.contrib.auth.decorators import login_required
# Create your views here.
import re
from PIL import Image,ImageDraw,ImageFont


def get_random():
    return random.randint(0,255),random.randint(0,255),random.randint(0,255)


def get_code(request):
    img_obj = Image.new('RGB',(500,34),get_random())
    img_draw = ImageDraw.Draw(img_obj)
    img_font = ImageFont.truetype('static/abc.ttf', 30)

    code = ''
    for i in range(5):
        random_upper = chr(random.randint(65, 90))
        random_lower = chr(random.randint(97, 122))
        random_int = str(random.randint(0, 9))
        tmp = random.choice([random_upper,random_lower,random_int])
        img_draw.text((i*60, 0), tmp, get_random(), img_font)
        code += tmp
    print(code)
    request.session['code'] = code
    io_obj = BytesIO()
    img_obj.save(io_obj,'png')
    return HttpResponse(io_obj.getvalue())


def login(request):
    back_dic = {"code": 1000, "msg": ''}
    if request.method == 'POST':
        username = request.POST.get('username')
        password = request.POST.get('password')
        vcode = request.POST.get('vcode')
        if vcode.upper() == request.session.get('code').upper() or vcode == '123456':
            user_obj = auth.authenticate(username=username, password=password)
            if user_obj:
              auth.login(request, user_obj)
              back_dic['url'] = '/home/'
            else:
              back_dic['code'] = '1001'
              back_dic['msg'] = '用户名或密码错误'
        else:
            back_dic['code'] = '1002'
            back_dic['msg'] = '验证码错误'
        return JsonResponse(back_dic)
    return render(request, 'login.html')


def register(request):
    back_dic = {"code": 1000, "msg": ''}
    if request.method == 'POST':
        username = request.POST.get('username')
        password = request.POST.get('password')
        email = request.POST.get('email')

        user = User.objects.filter(username=username)
        if user:
            back_dic['code'] = '1001'
            back_dic['msg'] = '用户已注册'
        else:
            email_re = re.match(r'^[0-9a-zA-Z_]{0,19}@[0-9a-zA-Z]{1,13}\.[0-9a-zA-Z]{1,3}$', email)
            if email_re:
                User.objects.create_user(username=username, password=password, email=email)
                back_dic['code'] = '1002'
                back_dic['msg'] = '注册成功'
            else:
                back_dic['code'] = '1003'
                back_dic['msg'] = '邮箱格式不正确'
        return JsonResponse(back_dic)
    return render(request, 'register.html')


@login_required(login_url='/login/')
def logout(request):
    auth.logout(request)
    return redirect('/login/')


@login_required(login_url='/login/')
def home(request):
    return render(request, 'home.html')


@login_required(login_url='/login/')
def set_password(request):
    back_dic = {'coe':1000, 'msg':''}
    if request.method == 'POST':
        old_password = request.POST.get('old_password')
        new_password = request.POST.get('new_password')
        confirm_password = request.POST.get('confirm_password')

        is_check = request.user.check_password(old_password)
        if is_check:
            if new_password == confirm_password:
                request.user.set_password(new_password)
                request.user.save()
                back_dic['code'] = '1000'
                back_dic['msg'] = '修改成功'

            else:
                back_dic['code'] = '1001'
                back_dic['msg'] = '两次密码不一致'
        else:
            back_dic['code'] = '1002'
            back_dic['msg'] = '原密码错误'
        return JsonResponse(back_dic)

    return render(request,'set_password.html',locals())
```

home.html

```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link  rel="stylesheet" href="/static/bootstrap.css">
    <script src="/static/jquery.js"></script>
    <script src="/static/bootstrap.js"></script>
</head>
<body>

<nav class="navbar navbar-inverse">
  <div class="container-fluid">
    <!-- Brand and toggle get grouped for better mobile display -->
    <div class="navbar-header">
      <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1" aria-expanded="false">
        <span class="sr-only">Toggle navigation</span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
      </button>
      <a class="navbar-brand" href="#">运 维 平 台</a>
    </div>
    <!-- Collect the nav links, forms, and other content for toggling -->
    <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
      <ul class="nav navbar-nav navbar-right">
        <li><a href="#">用户名称</a></li>
        <li class="dropdown">
          <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">操作<span class="caret"></span></a>
          <ul class="dropdown-menu">
            <li><a href="#">头像设置</a></li>
            <li><a href="/set_password/">修改密码</a></li>
            <li><a href="#">更多设置 </a></li>
            <li role="separator" class="divider"></li>
            <li><a href="/logout/">退出登录</a></li>
          </ul>
        </li>
      </ul>
    </div><!-- /.navbar-collapse -->
  </div><!-- /.container-fluid -->
</nav>

<div class="container-fluid">
    <div class="row">
        <div class="col-md-3">
            侧边栏
        </div>
        <div class="col-md-9">
            主页面
        </div>
    </div>
</div>

</body>
</html>
```

login.html

```sh
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link  rel="stylesheet" href="/static/bootstrap.css">
    <script src="/static/jquery.js"></script>
    <script src="/static/bootstrap.js"></script>
</head>
<body>

<div class="container">
    <div class="row">
        <div class="col-md-8 col-md-offset-2" style="margin-top: 100px">
            <h1 class="text-center">运 维 管 理 平 台</h1>
            <div class="form-group">
                <label for="username">用户名</label>
                <input type="text" name="username" id="username" class="form-control">
            </div>
            <div class="form-group">
                <label for="password">密码</label>
                <input type="password" name="password" id="password" class="form-control">
            </div>
            <div class="form-group">
                <label for="">验证码</label>
                <div class="row">
                    <div class="col-md-6">
                        <input type="text" name="vcode" id="vcode" class="form-control">
                    </div>
                    <div class="col-md-6">
                        <img src="/get_code/" alt="" width=99% height="34" id="id_img">
                    </div>

                </div>
            </div>
            <input type="button" class="btn btn-primary form-control" value="登 录" id="id_login">
            <span style="color: red" id="error"></span>
        </div>
    </div>
</div>

<script>
    $("#id_img").click(function () {

        let oldVal = $(this).attr('src');
        $(this).attr('src',oldVal += '?');
    })

    $('#id_login').click(function () {
        $.ajax({
            url: '/login/',
            type: 'post',
            data:{
                'username':$("#username").val(),
                'password':$("#password").val(),
                'vcode':$("#vcode").val(),
                'csrfmiddlewaretoken':'{{ csrf_token }}'
            },
            success: function (args){
                if(args.code == 1000){
                    window.location.href = args.url
                }else{
                    $('#error').text(args.msg)
                }
            }
        })

    })
</script>

</body>
</html>
```

register.html

```sh
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="/static/bootstrap.css">
    <script src='/static/jquery.js'></script>
    <script src="/static/bootstrap.js"></script>
</head>
<body>

<div class="container">
    <div class="row">
        <div class="col-md-8 col-md-offset-2">
            <h1 class="text-center">注册</h1>
            <div class="form-group">
                <label for="username">用户名</label>
                <input type="text" name="username" id="username" class="form-control">
            </div>
            <div class="form-group">
                <label for="password">密码</label>
                <input type="password" name="password" id="password" class="form-control">
            </div>
            <div class="form-group">
                <label for="email">邮箱</label>
                <input type="text" name="email" id="email" class="form-control">
            </div>
            <input type="button" class="btn btn-success pull-right" value="注册" id="id_register">
            <span style="color: red;font-size: 18px" id="error"></span>
        </div>
    </div>

</div>
<script>
    $('#id_register').click(function () {
        $.ajax({
            url: '/register/',
            type: 'post',
            data:{
                'username':$("#username").val(),
                'password':$("#password").val(),
                'email':$("#email").val(),
                'csrfmiddlewaretoken':'{{ csrf_token }}'
            },
            success: function (args){
                if(args.code == 1002){
                    alert('注册成功，跳转到登录页面')
                    window.location.href = '/login/'
                }else{
                    $('#error').text(args.msg)
                }
            }
        })

    })
</script>
</body>
</html>
```

setpassword.html

```sh
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="/static/bootstrap.css">
    <script src='/static/jquery.js'></script>
    <script src="/static/bootstrap.js"></script>
</head>
<body>

<div class="container">
    <div class="row">
        <div class="col-md-8 col-md-offset-2">
            <h1 class="text-center">修改密码</h1>
            <div class="form-group">
                <label for="username">用户名</label>
                <input type="text" name="username" disabled id="username" class="form-control" value="{{ request.user.username }}">
            </div>
            <div class="form-group">
                <label for="old_password">原密码</label>
                <input type="password" name="old_password" id="old_password" class="form-control">
            </div>
            <div class="form-group">
                <label for="new_password">新密码</label>
                <input type="password" name="new_password" id="new_password" class="form-control">
            </div>
            <div class="form-group">
                <label for="confirm_password">确认密码</label>
                <input type="password" name="confirm_password" id="confirm_password" class="form-control">
            </div>
            <input type="button" class="btn btn-success pull-right" value="修改" id="id_setpassword">
            <span style="color: red;font-size: 18px" id="password_error"></span>
        </div>
    </div>

</div>
<script>
    $('#id_setpassword').click(function () {
        $.ajax({
            url: '/set_password/',
            type: 'post',
            data:{
                'old_password':$("#old_password").val(),
                'new_password':$("#new_password").val(),
                'confirm_password':$("#confirm_password").val(),
                'csrfmiddlewaretoken':'{{ csrf_token }}'
            },
            success: function (args){
                if(args.code == 1000){
                    window.location.href = '/login/'
                }else{
                    $('#password_error').text(args.msg)
                }
            }
        })

    })
</script>
</body>
</html>
```



### 路由功能

```python
django1.X 用的url方法
django2.X和3.X 用的path方法
url第一个参数支持正则，path第一个参数不支持正则

在django2.X使用url方法
from  django.urls import path, re_path
from django.conf.urls import url
```

```python
#首页 url(r'^$', views.home)

#无名分组
url(r'^test/(\d+)' ,views.test)
def test(request,xx):
    print(xx)
    return HttpResponse(xx)
无名分组就是将括号内正则表达式匹配到的内容当做位置参数传递给后面函数

#有名分组
可以给正则表达式起一个别名
url(r'^test/(?P<year>\d+)/', views.test)
def test(request,year):
    print(year)
    return HttpResponse(year)
有名分组就是将括号内正则表达式匹配到的内容当做关键字参数传递给后面视图函数

#反向解析
url(r'^test/', views.test ,name='ooo')
def test(request):
    print(reverse('ooo'))
    return HttpResponse(reverse('ooo'))
<a href='{% url 'ooo' %}'></a>
```

```python
路由分发
根项目配置：
from django.conf.urls import url,include
from django.contrib import admin

import app01
from app01 import urls

urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'^app01/', include(app01.urls))
]

子项目配置：
from django.conf.urls import url
from app01 import views

urlpatterns = [
    url(r'^reg/',views.reg)
]
```



### module模型层

**filter括号内多个参数是and关系，若用要or,需要Q查询**

##### 操作ORM查看内部sql语句

第一种方式：QuerySet查询

```sh
res = models.User.objects.values_list("name")
print(res)  # <QuerySet [('jakes',), ('fer2',), ('fer3',), ('fer3',), ('fer1',)]>
print(res.query)

# 输出
SELECT `app01_user`.`name` FROM `app01_user`
```

第二种方式：所有sql语句，配置文件加入以下代码

```sh
LOGGING = {
    'version': 1,
    'disable_existing_loggers': False,
    'handlers': {
        'console':{
            'level':'DEBUG',
            'class':'logging.StreamHandler',
        },
    },
    'loggers': {
        'django.db.backends': {
            'handlers': ['console'],
            'propagate': True,
            'level':'DEBUG',
        },
    }
}
```



##### test文件

```sh
from django.test import TestCase
import os
import sys

if __name__ == "_main__":
    os.environ.setdefault("DJANGO_SETTINGS_MODULE", "test1.settings")
    import django
    django.setup()
    from app01 import models

    a = models.UserInfo.objects.all()
    print(a)
```

```sh
class.User(models:Model);
   name = models.CharField(max_length=32)
   age = models.IntegerField()
   register_time = models.DateField()#年月日" " "

DateField
DateTimeField
   两个重要参数
   auto_nbw :每次操作数据的时候该字段会自动将当前时间更新
   auto_now_add :在创建数据的时候会自动将当前创建时间记录下来之后只要不认为的修改那么就一直不变
```



##### 单表查询

```python
class.User(models:Model);
   name = models.CharField(max_length=32)
   age = models.IntegerField()
   register_time = models.DateField()#年月日" " "

DateField
DateTimeField
   两个重要参数
   auto_nbw :每次操作数据的时候该字段会自动将当前时间更新
  auto_now_add :在创建数据的时候会自动将当前创建时间记录下来之后只要不认为的修改那么就一直不变
  

查询所有数据
a = models.User.objects.all()
for i in a:
    print(i.name,i.age)  
  
1、增加数据 
res = models.User.objects.create(name='bbb',age='14',register_time='2020-11-11')
print(res)

2、增加数据
import  datetime
ctime = datetime.datetime.now()
user_obj = models.User(name='aass',age=111,register_time=ctime)
user_obj.save()
print(user_obj)

3、删除数据
res = models.User.objects.filter(pk=3).delete()
print(res)

4、删除数据
res = models.User.objects.filter(pk=2).first()
res.delete()

5、修改数据
models.User.objects.filter(pk=1).update(name='nihao')

6、取第一个和最后一个
res = models.User.objects.all().first()
res = models.User.objects.all().last()

7、values 获取某一列
res = models.User.objects.values('name')
res = models.User.objects.values('name','age')
################
....<QuerySet [{'name':'jason'}, {'name':'egonPPP'}]>

8.values_list()列表套元祖
res = models.User.objects.values_list( 'name','age')

9.distinct()去重
res = models.User.objects.values('name','age').distinct()

9.order_by
res = models.User.objects.order_by('age')  #默认升序
res = models.User.objects.order_by('-age')  #降序

10.reverse()反转的前提是数据已经排过序了order_by()
res1 = models.User.objects.order_by( 'age ' ).reverse()

11.count()统计当前数据的个数
res = models.User.objects.count()

12.exclude()排除在外
res = models.User.objects.exclude(name= 'jason ')
```



##### 双下划线查询

```sh
1、年龄大于35岁的数据
res =rmodels.User.objects.filter(age._gt=35)

2、年龄小于35岁的数据
res = models.User.objects.filter(age__lt=35)

3、大于等于小于等于
res = models.User.objects.filter(age__gte=32)

4、年龄是18或者32或者40
res = models.User.objects.filter(age__in=[18,32,40])

5、年龄在18到40岁之间的首尾都要
res = models.User.objects.filter(age._range=[18,40])

6、查询出名字里面含有s的数据模糊查询
res = models.User.objects.filter(name__contains='s')

7、开始 结尾
res = models.User.objects.filter(name_startswith='j')
res1 = models.User.objects.filter(name__endswith='j')

8、查询出注册时间是.2920.1月
res = models.User.objects.filter(register_time__month='1')
res = models.User.objects.filter(register_time__year='2020')
```



##### 一对多

```sh
class Book(models.Model):
    title = models.CharField(max_length=50)
    price = models.DecimalField(max_digits=8,decimal_places=2)
    publish_data = models.DateField(auto_now_add=True)

    #一对多
    publish = models.ForeignKey(to='Publish')

    #多对多
    authors = models.ManyToManyField(to='Author')

class Publish(models.Model):
    name = models.CharField(max_length=50)
    addr = models.CharField(max_length=100)
    email = models.EmailField()

class Author(models.Model):
    name = models.CharField(max_length=33)
    age = models.IntegerField()
    author_detail = models.OneToOneField(to='AuthorDetail')

class AuthorDetail(models.Model):
    phone = models.BigIntegerField()
    addr = models.CharField(max_length=44)
```





# 项目一：博客

#### 表结构

```python
"""
1、用户表
   继承AbstractUser
   拓展
     phone  电话号码
     avatar 头像
     create_time  创建时间
   外键字段
     一对一个人站点
   
2、个人站点表
     site_name 站点名称 
     site_title 站点标题
     stie_thema  站点主题
   

3、文章标签表
     name 标签名
   外键字段：
     一对多个人站点


4、文章分类表
   name  分类
   外键字段：
      一对多个人站点
      

5、文章表
   title 文章标题
   desc  简介
   content  内容
   create_time 发布时间
   
   设计优化：（虽然可以跨表查询，效率低）
   点赞数 up_num  
   点踩数 down_num
   评论数 comment_num
   
   外键字段：
      一对多 个人站点
      多对多 标签
      一对多 分类

6、 点赞点踩表
    记录那个用户给那个文章点赞还是点踩
    user 用户主键  ForeignKey(to='User')
    article 文章主键  ForeignKey(to='Article')
    is_up   Boolen
    
    

7、评论表 
   user   ForeignKey(to='User')
   article  ForeignKey(to='Article')
   content
   comment_time
   
   根评论 子评论
   
"""
```

```sh
from django.db import models
from django.contrib.auth.models import User, AbstractUser



class UserInfo(AbstractUser):
    phone = models.BigIntegerField(verbose_name='手机号',null=True)
    avatar = models.FileField(upload_to='avatar/', default='avatar/default.png')
    create_time = models.DateField(auto_now_add=True)

    blog = models.OneToOneField(to='Blog',null=True)

class Blog(models.Model):
    site_name =  models.CharField(max_length=32,verbose_name='站点名称')
    site_title = models.CharField(max_length=32,verbose_name='站点标题')
    site_thema = models.CharField(max_length=128,verbose_name='站点样式')

class Category(models.Model):
    name = models.CharField(max_length=32,verbose_name='文章分类')
    blog = models.ForeignKey(to='Blog',null=True)

class Tag(models.Model):
    name = models.CharField(max_length=32,verbose_name='文章标签')
    blog = models.ForeignKey(to='Blog',null=True)

class Article(models.Model):
    title = models.CharField(max_length=32,verbose_name='文章标题')
    desc = models.CharField(max_length=128,verbose_name='文章简介')
    content = models.TextField(verbose_name='文章内容')
    create_time = models.DateField(auto_now_add=True)

    up_num = models.BigIntegerField(verbose_name='点赞数',default=0)
    down_num = models.BigIntegerField(verbose_name='点踩数',default=0)
    comment_num = models.BigIntegerField(verbose_name='评论数',default=0)

    blog = models.ForeignKey(to='Blog',null=True)
    category = models.ForeignKey(to='Category',null=True)
    tags = models.ManyToManyField(to='Tag',through='Article2Tag',through_fields=('article','tag'))

class Article2Tag(models.Model):
    article = models.ForeignKey(to='Article')
    tag = models.ForeignKey(to='Tag')


class UpAndDown(models.Model):
    user = models.ForeignKey(to='UserInfo')
    article = models.ForeignKey(to="Article")
    is_up = models.BooleanField()

class Comment(models.Model):
    user = models.ForeignKey(to='UserInfo')
    article = models.ForeignKey(to='Article')
    conent = models.CharField(max_length=256,verbose_name='评论内容')
    comment_time = models.DateTimeField(auto_now_add=True)

    parent = models.ForeignKey(to="self",null=True)
```

#### 基本配置

init文件配置

```sh
import pymysql
pymysql.install_as_MySQLdb()
```

settings文件配置

```sh
`1、html末班配置`
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [os.path.join(BASE_DIR,'template')],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]


`2\数据库配置`
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'bbs',
        'USER': 'root',
        'PASSWORD': '123456',
        'HOST': '10.0.0.11',
        'PORT': 3306,
        'CHARSET': 'utf8'
    }
}


`3、静态文件配置`
STATIC_URL = '/static/'
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, "static"),  # 静态文件存放位置
]

AUTH_USER_MODEL = 'app01.UserInfo'
```



#### 注册功能

```sh
from django.shortcuts import render
from django.http import HttpResponse,JsonResponse
import re
from app01 import models


def register(request):

    back_dic = {'msg':'','code':1000}

    if request.method =="POST":
        username = request.POST.get("username")
        password = request.POST.get("password")
        confirm_password = request.POST.get("confirm_password")
        email = request.POST.get("email")
        phone = request.POST.get("phone")
        avatar_file = request.FILES.get("file_obj")

        user = models.UserInfo.objects.filter(username=username)

        if username:
            if user:
                back_dic['code'] = '1001'
                back_dic['msg'] = '用户已注册'
            else:
                email_re = re.match(r'^[0-9a-zA-Z_]{0,19}@[0-9a-zA-Z]{1,13}\.[0-9a-zA-Z]{1,3}$', email)
                if email_re:
                    if password == confirm_password:
                         models.UserInfo.objects.create_user(username=username,password=password,phone=phone,avatar=avatar_file)
                        back_dic['code'] = '1002'
                        back_dic['msg'] = '注册成功'
                    else:
                        back_dic['code'] = '1003'
                        back_dic['msg'] = '两次密码不一致'
                else:
                    back_dic['code'] = '1004'
                    back_dic['msg'] = '邮箱格式不正确'
        else:
            back_dic['code'] = '1005'
            back_dic['msg'] = '用户名为空'
        return JsonResponse(back_dic)

    return render(request,'register.html')
```

```sh
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="/static/css/bootstrap.css">
    <script src='/static/jquery-3.6.0.js'></script>
    <script src="/static/js/bootstrap.js"></script>
</head>
<body>

<div class="container">
    <div class="row">
        <div class="col-md-8 col-md-offset-2">
            <h1 class="text-center">注册</h1>
            <div class="form-group">
                <label for="username">用户名</label>
                <input type="text" name="username" id="username" class="form-control">
            </div>
            <div class="form-group">
                <label for="password">密码</label>
                <input type="text" name="password" id="password" class="form-control">
            </div>
            <div class="form-group">
                <label for="confirm_password">确认密码</label>
                <input type="text" name="confirm_password" id="confirm_password" class="form-control">
            </div>
            <div class="form-group">
                <label for="email">邮箱</label>
                <input type="text" name="email" id="email" class="form-control">
            </div>
            <div class="form-group">
                <label for="phone">手机号</label>
                <input type="text" name="phone" id="phone" class="form-control">
            </div>
            <div class="form-group">
                <label for="myfile">头像
                    <img src="/static/default.jpg" alt="" id="myimg" style="width: 80px;height: 80px">
                </label>
                <input type="file" name="avatar" id="myfile" style="display: none">
            </div>

            <input type="button" class="btn btn-success pull-right" value="注册" id="id_register">
            <span style="color: red;font-size: 18px" id="error"></span>
        </div>
    </div>

</div>
<script>

    $("#myfile").change(function (){
        let myFileReaderObj = new FileReader();
        let fileObj = $(this)[0].files[0];
        myFileReaderObj.readAsDataURL(fileObj);
        myFileReaderObj.onload = function (){
            $('#myimg').attr('src',myFileReaderObj.result)
        }

    })

    $('#id_register').click(function () {

        var username = $("#username").val();
        var password = $("#password").val();
        var confirm_password = $("#confirm_password").val();
        var email = $("#email").val();
        var phone = $("#phone").val();
        var file = $("#myfile")[0].files[0];
        var formadate = new FormData();

        formadate.append('username', username);
        formadate.append('password', password);
        formadate.append('confirm_password', confirm_password);
        formadate.append('email', email);
        formadate.append('phone', phone);
        formadate.append('file_obj', file);
        formadate.append('csrfmiddlewaretoken','{{ csrf_token }}');

        $.ajax({
            url: '/register/',
            type: 'post',
            processData: false,
            contentType: false,
            data: formadate,
            success: function (args){
                if(args.code == 1002){

                    window.location.href = '/login/'
                }else{
                    $('#error').text(args.msg)
                }
            }
        })
    })
</script>
</body>
</html>
```



#### 登录功能

图形验证码

```sh
BytesIO: 临时存取数据 返回二进制数据
StringIO: 临时存取数据 返回字符串
```

```sh
import random

from django.http import JsonResponse
from django.shortcuts import render, HttpResponse
from PIL import Image, ImageDraw, ImageFont
from io import StringIO, BytesIO
from django.contrib import auth
from app01 import  models
from app01.models import UserInfo


def register():
    user = UserInfo.objects.create_user(username='jianli',password='12345',email='23234@qww.com',create_time='2020-11-12')

register()


def login(request):
    if request.method == 'POST':
        back_dic = {'code':1000,'msg':''}
        username = request.POST.get('username')
        password = request.POST.get('password')
        code = request.POST.get('code')

        if request.session.get('code').upper() == code.upper():
            user_obj = auth.authenticate(request,username=username,password=password)
            if user_obj:
                auth.login(request,user_obj)
                back_dic['url'] = '/home/'
            else:
                back_dic['code'] = 2000
                back_dic['msg'] = '用户名密码错误'
        else:
            back_dic['code'] = 3000
            back_dic['msg'] = '验证码错误'
        return JsonResponse(back_dic)


    return render(request, 'login.html')


def get_random():
    import random
    return random.randint(0, 255), random.randint(0, 255), random.randint(0, 255)


def get_code(request):
    # 步骤一 文件读取
    # with open(r'C:\Users\Administrator\PycharmProjects\djangoProject1\avatar\default.jpg','rb') as f:
    #    data = f.read()
    # return HttpResponse(data)

    # 步骤二  生成图片
    # image_obj = Image.new('RGB',(430,34),get_random())
    # #保存图片
    # with open('xxx.png','wb') as f:
    #     image_obj.save(f,'png')
    # with  open('xxx.png','rb') as f:
    #     data = f.read()
    # return HttpResponse(data)

    # 步骤三  内存存取图片
    # image_obj = Image.new('RGB',(500,34),get_random())
    # io_obj = BytesIO()
    # image_obj.save(io_obj,'png')
    # return HttpResponse(io_obj.getvalue())

    # 生成文字
    img_obj = Image.new('RGB', (500, 34), get_random())
    img_draw = ImageDraw.Draw(img_obj)  #产生画笔对象
    img_font = ImageFont.truetype('static/abc.ttf', 30) #字体样式 大小

    # 随机验证码
    code = ''
    for i in range(5):
        random_upper = chr(random.randint(65, 90))
        random_lower = chr(random.randint(97, 122))
        random_int = str(random.randint(0, 9))
        tmp = random.choice([random_int, random_upper, random_lower])
        # 为什么一个个生成好再写  可以控制字体间隙
        img_draw.text((i*60, 0), tmp, get_random(), img_font)
        code += tmp
    print(code)
    request.session['code'] = code
    io_obj = BytesIO()
    img_obj.save(io_obj, 'png')
    return HttpResponse(io_obj.getvalue())
```

```sh
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="/static/bootstrap.css">
    <script src="/static/jquery-3.5.1.js"></script>
    <script src="/static/bootstrap.js"></script>
</head>
<body>

<div class="container">
    <div class="row">
        <div class="col-md-8 col-md-offset-2" style="margin-top: 100px">

            <h1 class="text-center">运 维 管 理 平 台</h1>
            <div class="form-group">
                <label for="username">用户名</label>
                <input type="text" name="username" id="username" class="form-control">
            </div>
            <div class="form-group">
                <label for="password">密码</label>
                <input type="password" name="password" id="password" class="form-control">
            </div>
            <div class="form-group">
                <label for="">验证码</label>
                <div class="row">
                    <div class="col-md-6">
                        <input type="text" name="vcode" id="vcode" class="form-control">
                    </div>
                    <div class="col-md-6">
                        <img src="/get_code/" alt="" width=99% height="34" id="id_img">
                    </div>

                </div>
            </div>
            <input type="button" class="btn btn-primary form-control" value="登 录" id="id_login">
            <span style="color: red" id="error"></span>
        </div>
    </div>
</div>

<script>
    $("#id_img").click(function () {

        let oldVal = $(this).attr('src');
        $(this).attr('src',oldVal += '?');
    })

    $('#id_login').click(function () {
        $.ajax({
            url: '/login/',
            type: 'post',
            data:{
                'username':$("#username").val(),
                'password':$("#password").val(),
                'vcode':$("#vcode").val(),
                'csrfmiddlewaretoken':'{{ csrf_token }}'
            },
            success: function (args){
                if(args.code == 1000){
                    window.location.href = args.url
                }else{
                    $('#error').text(args.msg)
                }
            }
        })
    })
</script>
</body>
</html>
```



#### 导航条 

```sh
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="/static/bootstrap.min.css">
    <script src="/static/jquery-3.5.1.js"></script>
    <script src="/static/bootstrap.min.js"></script>
</head>
<body>

<nav class="navbar navbar-default">
  <div class="container-fluid">
    <!-- Brand and toggle get grouped for better mobile display -->
    <div class="navbar-header">
      <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1" aria-expanded="false">
        <span class="sr-only">Toggle navigation</span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
      </button>
      <a class="navbar-brand" href="#">博客 </a>
    </div>

    <!-- Collect the nav links, forms, and other content for toggling -->
    <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
      <ul class="nav navbar-nav">
        <li class="active"><a href="#"> <span class="sr-only">(current)</span></a></li>
        <li><a href="#">文章 </a></li>
>

        <li class="dropdown">
          <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">更多 <span class="caret"></span></a>
          <ul class="dropdown-menu">
            <li><a href="#">Action</a></li>
            <li><a href="#">Another action</a></li>
            <li><a href="#">Something else here</a></li>
            <li role="separator" class="divider"></li>
            <li><a href="#">Separated link</a></li>
            <li role="separator" class="divider"></li>
            <li><a href="#">One more separated link</a></li>
          </ul>
        </li>
      </ul>
      <form class="navbar-form navbar-left">
        <div class="form-group">
          <input type="text" class="form-control" placeholder="Search">
        </div>
        <button type="submit" class="btn btn-default">Submit</button>
      </form>
      <ul class="nav navbar-nav navbar-right">
          {% if request.user.is_authenticated %}
               <li><a href="#">{{ request.user.username }}</a></li>
        <li class="dropdown">
          <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">更过操作 <span class="caret"></span></a>
          <ul class="dropdown-menu">
            <li><a href="#">修改密码</a></li>
            <li><a href="#">修改头像</a></li>
            <li><a href="#">后台管理</a></li>
            <li role="separator" class="divider"></li>
            <li><a href="#">退出登录</a></li>
          </ul>
        </li>

          {% else %}
               <li><a href="#">注册</a></li>
               <li><a href="/login/">登录</a></li>
          {% endif %}

      </ul>
    </div><!-- /.navbar-collapse -->
  </div><!-- /.container-fluid -->
</nav>

</body>
</html>
```



#### 修改密码和注销

```sh
@login_required()
def logout(request):
    auth.logout(request)
    return redirect('/home/')

@login_required()
def set_password(request):
    back_dic = {"code": 1000, "msg": ''}

    if request.method == 'POST':
        username = request.POST.get('username')
        old_password = request.POST.get('old_password')
        new_password = request.POST.get('new_password')
        confirm_password = request.POST.get('confirm_password')

        is_right = request.user.check_password(old_password)
        if is_right:
            if new_password == confirm_password:
                request.user.set_password(new_password)
                request.user.save()
            else:
                back_dic['code'] = '1001'
                back_dic['msg'] = '密码不一致'
        else:
            back_dic['code'] = '1002'
            back_dic['msg'] = '原密码错误'
        return JsonResponse(back_dic)

    return render(request,'set_password.html')
```

```sh
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
        <link rel="stylesheet" href="/static/bootstrap.css">
    <script src="/static/jquery-3.5.1.js"></script>
    <script src="/static/bootstrap.js"></script>
</head>
<body>

<div class="container-fluid">
    <div class="row">
        <div class="col-md-8 col-md-offset-2">
            <h1>修改密码</h1>
            <div class="form-group">
                {% csrf_token %}
                <label for="username">用户名</label>
                <input type="text" disabled value="{{ request.user.username }}" class="form-control">
            </div>
            <div class="form-group">
                <label for="old_password">原密码</label>
                <input type="password" name="old_password" id="old_password" class="form-control">
            </div>
             <div class="form-group">
                <label for="new_password">新密码</label>
                <input type="password" name="new_password" id="new_password" class="form-control">
            </div>
             <div class="form-group">
                <label for="confirm_password">确认密码</label>
                <input type="password" name="confirm_password" id="confirm_password" class="form-control">
            </div>

            <input type="button" class="btn btn-primary form-control" value="修改" id="id_edit">
            <span style="color: red" id="password_error"></span>

        </div>
    </div>
</div>
<script>
    $('#id_edit').click(function (){
        $.ajax({
            url:'/set_password/',
            type: 'post',
            data:{
                'old_password':$('#old_password').val(),
                'new_password':$('#new_password').val(),
                'confirm_password':$('#confirm_password').val(),
                'csrfmiddlewaretoken': '{{ csrf_token }}'
            },
            success:function (args){
                if (args.code == 1000){
                    window.location.href = '/home/'
                }else{
                    $("#password_error").text(args.msg)
                }
            }
        })
    })
</script>

</body>
</html>
```



#### admin后台管理

引入admin

```sh
from django.contrib import admin
from app01 import  models
admin.site.register(models.UserInfo)
```

修改admin后台表名字

```sh
class UserInfo(AbstractUser):
    phone = models.BigIntegerField(verbose_name='手机号',null=True)
    avatar = models.FileField(upload_to='avatar/',default='avatar/default.jpg')
    create_time = models.DateField(auto_created=True,null=True)
    blog = models.OneToOneField(to='Blog',null=True,on_delete=models.CASCADE)
    
    class Meta:
        verbose_name_plural = '用户表'
```

x修改密码

```sh
from django.contrib.auth.models import User
u = User.objects.get(username='your_name')
u.set_password('new_password')
u.save()
```





#### 自定义上传静态media路径

URL文件中如下

```sh
from django.conf import settings
from django.urls import re_path
from django.views.static import serve

# ... the rest of your URLconf goes here ...

if settings.DEBUG:
    urlpatterns += [
        re_path(r'^media/(?P<path>.*)$', serve, {
            'document_root': settings.MEDIA_ROOT,
        }),
    ]
```

settings文件中如下

```sh
MEDIA_ROOT = os.path.join(BASE_DIR,'media')
```





#### home页面配置

```sh
def home(request):
    article_queryset = models.Article.objects.all()
    return render(request,'home.html',locals())
```

```html

<div class="container-fluid">
    <div class="col-md-2">
        <div class="panel panel-default">
            <div class="panel-heading">
                <h3 class="panel-title">模板主题一</h3>
            </div>
            <div class="panel-body">
                信息 message
            </div>
        </div>
         <div class="panel panel-danger">
            <div class="panel-heading">
                <h3 class="panel-title">模板主题二</h3>
            </div>
            <div class="panel-body">
                信息 message
            </div>
        </div>
        <div class="panel panel-success">
            <div class="panel-heading">
                <h3 class="panel-title">模板主题三</h3>
            </div>
            <div class="panel-body">
                信息 message
            </div>
        </div>
    </div>
    <div class="col-md-8">
        <ul class="media-list">
            {% for article_obj in article_queryset %}
                <li class="media">
                <h4 class="media-heading"><a href="">{{ article_obj.title }}</a></h4>
                <div class="media-left">
                    <a href="#">
                        <img class="media-object" style="width: 80px;height: 80px" src="/media/{{article_obj.blog.userinfo.avatar}}" alt="...">
                    </a>
                </div>
                <div class="media-body">

                     {{ article_obj.desc }}
                </div>
                <div>
                    <span><a href="">{{ article_obj.blog.userinfo.username }}</a></span>
                    <span>发布于</span>
                    <span>{{ article_obj.create_time|date:'Y-m-d' }}</span>
                    <span><span class="glyphicon glyphicon-comment"></span>评论({{ article_obj.comment_num }})</span>
                    <span><span class="glyphicon glyphicon-thumbs-up"></span>点赞({{ article_obj.up_num }})</span>
                </div>
            </li>
            <hr>
            {% endfor %}
        </ul>
    </div>
    <div class="col-md-2">
         <div class="panel panel-default">
            <div class="panel-heading">
                <h3 class="panel-title">模板主题一</h3>
            </div>
            <div class="panel-body">
                信息 message
            </div>
        </div>
         <div class="panel panel-danger">
            <div class="panel-heading">
                <h3 class="panel-title">模板主题二</h3>
            </div>
            <div class="panel-body">
                信息 message
            </div>
        </div>
        <div class="panel panel-success">
            <div class="panel-heading">
                <h3 class="panel-title">模板主题三</h3>
            </div>
            <div class="panel-body">
                信息 message
            </div>
        </div>
    </div>
</div>
```



#### 个人站点

```sh
re_path(r'^(?P<username>\w+)/$',views.site),
```

```sh
def site(request,username):
    user_obj = models.UserInfo.objects.filter(username=username).first()
    if not  user_obj:
        return render(request,'error.html')
    blog = user_obj.blog
    article_list = models.Article.objects.filter(blog=blog)
    return render(request,'site.html',locals())
```

```sh
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
        <link rel="stylesheet" href="/static/bootstrap.css">
    <script src="/static/jquery-3.5.1.js"></script>
    <script src="/static/bootstrap.js"></script>
</head>
<body>
<nav class="navbar navbar-default">
    <div class="container-fluid">
        <!-- Brand and toggle get grouped for better mobile display -->
        <div class="navbar-header">
            <button type="button" class="navbar-toggle collapsed" data-toggle="collapse"
                    data-target="#bs-example-navbar-collapse-1" aria-expanded="false">
                <span class="sr-only">Toggle navigation</span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
            </button>
            <a class="navbar-brand" href="#">boke  </a>
        </div>

        <!-- Collect the nav links, forms, and other content for toggling -->
        <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
            <ul class="nav navbar-nav">
                <li class="active"><a href="#"> <span class="sr-only">(current)</span></a></li>
                <li><a href="#">文章 </a></li>

                <li class="dropdown">
                    <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true"
                       aria-expanded="false">更多 <span class="caret"></span></a>
                    <ul class="dropdown-menu">
                        <li><a href="#">Action</a></li>
                        <li><a href="#">Another action</a></li>
                        <li><a href="#">Something else here</a></li>
                        <li role="separator" class="divider"></li>
                        <li><a href="#">Separated link</a></li>
                        <li role="separator" class="divider"></li>
                        <li><a href="#">One more separated link</a></li>
                    </ul>
                </li>
            </ul>
            <form class="navbar-form navbar-left">
                <div class="form-group">
                    <input type="text" class="form-control" placeholder="Search">
                </div>
                <button type="submit" class="btn btn-default">Submit</button>
            </form>
            <ul class="nav navbar-nav navbar-right">
                {% if request.user.is_authenticated %}
                    <li><a href="#">{{ request.user.username }}</a></li>
                    <li class="dropdown">
                        <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true"
                           aria-expanded="false">更过操作 <span class="caret"></span></a>
                        <ul class="dropdown-menu">
                            <li><a href="/set_password/">修改密码</a></li>
                            <li><a href="#">修改头像</a></li>
                            <li><a href="#">后台管理</a></li>
                            <li role="separator" class="divider"></li>
                            <li><a href="/logout/">退出登录</a></li>
                        </ul>
                    </li>

                {% else %}
                    <li><a href="#">注册</a></li>
                    <li><a href="/login/">登录</a></li>
                {% endif %}

            </ul>
        </div><!-- /.navbar-collapse -->
    </div><!-- /.container-fluid -->
</nav>

<div class="container-fluid">
    <div class="row">
        <div class="col-md-3">
<div class="panel panel-default">
            <div class="panel-heading">
                <h3 class="panel-title">模板主题一</h3>
            </div>
            <div class="panel-body">
                信息 message
            </div>
        </div>
         <div class="panel panel-danger">
            <div class="panel-heading">
                <h3 class="panel-title">模板主题二</h3>
            </div>
            <div class="panel-body">
                信息 message
            </div>
        </div>
        <div class="panel panel-success">
            <div class="panel-heading">
                <h3 class="panel-title">模板主题三</h3>
            </div>
            <div class="panel-body">
                信息 message
            </div>
        </div>
        </div>
        <div class="col-md-9">
            <ul class="media-list">
                  {% for article_obj in article_list %}
                    <li class="media">
                        <h4 class="media-heading"><a href="#">{{ article_obj.title }}</a></h4>
                        <div class="media-left">
                            <a href="#">
                                <img class="media-object" style="width: 60px;height: 40px"  src="/media/{{article_obj.blog.userinfo.avatar}}" alt="...">
                            </a>
                        </div>
                        <div class="media-body">
                            {{ article_obj.desc }}
                        </div>
                        </br>
                        <div  class="pull-right">
                            <span>posted</span>
                            <span>@</span>
                            <span>{{ article_obj.create_time|date:'Y-m-d' }}</span>
                            <span><a href="#">{{ article_obj.blog.userinfo.username }}</a> </span>
                            <span><span class="glyphicon glyphicon-grain"></span>评论数({{ article_obj.comment_num }})</span>
                            <span><span class="glyphicon glyphicon-comment"></span>点赞数({{ article_obj.up_num }})</span>
                            <span><a href="#">编辑</a></span>
                        </div>
                    </li>
                      <hr>
                   {% endfor %}
                </ul>
        </div>
    </div>
</div>
</body>
</html>
```



#### 侧边栏

```python 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
        <link rel="stylesheet" href="/static/bootstrap.css">
    <script src="/static/jquery-3.5.1.js"></script>
    <script src="/static/bootstrap.js"></script>
    <link rel="stylesheet" href="/media/css/{{ blog.site_thema }}">
</head>
<body>
<nav class="navbar navbar-default">
    <div class="container-fluid">
        <!-- Brand and toggle get grouped for better mobile display -->
        <div class="navbar-header">
            <button type="button" class="navbar-toggle collapsed" data-toggle="collapse"
                    data-target="#bs-example-navbar-collapse-1" aria-expanded="false">
                <span class="sr-only">Toggle navigation</span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
            </button>
            <a class="navbar-brand" href="#">boke  </a>
        </div>

        <!-- Collect the nav links, forms, and other content for toggling -->
        <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
            <ul class="nav navbar-nav">
                <li class="active"><a href="#"> <span class="sr-only">(current)</span></a></li>
                <li><a href="#">文章 </a></li>

                <li class="dropdown">
                    <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true"
                       aria-expanded="false">更多 <span class="caret"></span></a>
                    <ul class="dropdown-menu">
                        <li><a href="#">Action</a></li>
                        <li><a href="#">Another action</a></li>
                        <li><a href="#">Something else here</a></li>
                        <li role="separator" class="divider"></li>
                        <li><a href="#">Separated link</a></li>
                        <li role="separator" class="divider"></li>
                        <li><a href="#">One more separated link</a></li>
                    </ul>
                </li>
            </ul>
            <form class="navbar-form navbar-left">
                <div class="form-group">
                    <input type="text" class="form-control" placeholder="Search">
                </div>
                <button type="submit" class="btn btn-default">Submit</button>
            </form>
            <ul class="nav navbar-nav navbar-right">
                {% if request.user.is_authenticated %}
                    <li><a href="#">{{ request.user.username }}</a></li>
                    <li class="dropdown">
                        <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true"
                           aria-expanded="false">更过操作 <span class="caret"></span></a>
                        <ul class="dropdown-menu">
                            <li><a href="/set_password/">修改密码</a></li>
                            <li><a href="#">修改头像</a></li>
                            <li><a href="#">后台管理</a></li>
                            <li role="separator" class="divider"></li>
                            <li><a href="/logout/">退出登录</a></li>
                        </ul>
                    </li>

                {% else %}
                    <li><a href="#">注册</a></li>
                    <li><a href="/login/">登录</a></li>
                {% endif %}

            </ul>
        </div><!-- /.navbar-collapse -->
    </div><!-- /.container-fluid -->
</nav>

<div class="container-fluid">
    <div class="row">
        <div class="col-md-3">
<div class="panel panel-default">
            <div class="panel-heading">
                <h3 class="panel-title">文章分类</h3>
            </div>
            <div class="panel-body">
                {% for category in category_list %}
                    <p>{{ category.0 }}({{ category.1 }})</p>
                {% endfor %}
            </div>
        </div>
         <div class="panel panel-danger">
            <div class="panel-heading">
                <h3 class="panel-title">文章标签</h3>
            </div>
            <div class="panel-body">
                {% for tag in tag_list %}
                    <p>{{ tag.0 }}({{ tag.1 }})</p>
                {% endfor %}
            </div>
        </div>
        <div class="panel panel-success">
            <div class="panel-heading">
                <h3 class="panel-title">文章归档</h3>
            </div>
            <div class="panel-body">
                {% for date1_list in date_list %}
                    <p>{{ date1_list.0|date:"Y年m月" }}({{ date1_list.1 }})</p>
                {% endfor %}
            </div>
        </div>
        </div>
        <div class="col-md-9">
            <ul class="media-list">
                  {% for article_obj in article_list %}
                    <li class="media">
                        <h4 class="media-heading"><a href="#">{{ article_obj.title }}</a></h4>
                        <div class="media-left">
                            <a href="#">
                                <img class="media-object" style="width: 60px;height: 40px"  src="/media/{{article_obj.blog.userinfo.avatar}}" alt="...">
                            </a>
                        </div>
                        <div class="media-body">
                            {{ article_obj.desc }}
                        </div>
                        </br>
                        <div  class="pull-right">
                            <span>posted</span>
                            <span>@</span>
                            <span>{{ article_obj.create_time|date:'Y-m-d' }}</span>
                            <span><a href="#">{{ article_obj.blog.userinfo.username }}</a> </span>
                            <span><span class="glyphicon glyphicon-grain"></span>评论数({{ article_obj.comment_num }})</span>
                            <span><span class="glyphicon glyphicon-comment"></span>点赞数({{ article_obj.up_num }})</span>
                            <span><a href="#">编辑</a></span>
                        </div>
                    </li>
                      <hr>
                   {% endfor %}
                </ul>
        </div>
    </div>
</div>
</body>
</html>
```

```sh
def site(request,username):

    user_obj = models.UserInfo.objects.filter(username=username).first()

    if not user_obj:
        return render(request,'404.html')
    blog = user_obj.blog

    #查询当前给人站点所有文章
    article_list = models.Article.objects.filter(blog=blog)

    #查询当前所有用户所有分类及分类下的文章数
    category_list = models.Category.objects.filter(blog=blog).annotate(count_num=Count('article__pk')).values_list('name','count_num')
    print(category_list)

    # 查询当前所有用户所有标签及标签下的文章数
    tag_list = models.Tag.objects.filter(blog=blog).annotate(count_num=Count('article__pk')).values_list(
        'name', 'count_num')
    print(tag_list)

    #日期归档
    date_list = models.Article.objects.filter(blog=blog).annotate(month=TruncMonth('create_time')).values(
        'month').annotate(count_num=Count('pk')).values_list('month', 'count_num')
    print(date_list)

    return render(request,'site.html',locals())
```



#### 侧边栏筛选功能

```sh
def article_detail(request,username,article_id):

    user_obj = models.UserInfo.objects.filter(username=username).first()
    blog = user_obj.blog

    # 查询当前所有用户所有分类及分类下的文章数
    category_list = models.Category.objects.filter(blog=blog).annotate(count_num=Count('article__pk')).values_list(
        'name', 'count_num', 'pk')
    print(category_list)

    # 查询当前所有用户所有标签及标签下的文章数
    tag_list = models.Tag.objects.filter(blog=blog).annotate(count_num=Count('article__pk')).values_list(
        'name', 'count_num', 'pk')
    print(tag_list)

    # 日期归档
    date_list = models.Article.objects.filter(blog=blog).annotate(month=TruncMonth('create_time')).values(
        'month').annotate(count_num=Count('pk')).values_list('month', 'count_num', 'pk')
    print(date_list)

    article_obj = models.Article.objects.filter(pk=article_id).first()
    if not article_obj:
        return render(request,'404.html')
    return render(request,'article_detail.html', locals())
```



#### 点赞点踩

```sh
点赞点踩
1 校验用户是否登录
2 判断当前文章是否时用户自己写
3 当前用户是否已点过赞
4 操作数据库
```

![image-20211112102606300](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20211112102606300.png)

```sh
{% extends 'sitebase.html' %}

{% block css %}
    <style>
    #div_digg {
    float: right;
    margin-bottom: 10px;
    margin-right: 30px;
    font-size: 12px;
    width: 125px;
    text-align: center;
    margin-top: 10px;
}
    .diggit {
    float: left;
    width: 46px;
    height: 52px;
    background: url(/static/img/upup.gif) no-repeat;
    text-align: center;
    cursor: pointer;
    margin-top: 2px;
    padding-top: 5px;
}
    .buryit {
    float: right;
    margin-left: 20px;
    width: 46px;
    height: 52px;
    background: url(/static/img/downdown.gif) no-repeat;
    text-align: center;
    cursor: pointer;
    margin-top: 2px;
    padding-top: 5px;
}
    .clear {
    clear: both;
}
    </style>
{% endblock %}
{% block content %}
     {% csrf_token %}
    <h1>{{ article_obj.title }}</h1>
    <div class="">
    {{ article_obj.content|safe }}
    </div>
    {# 点赞点踩开始 #}
    <div id="div_digg">
        <div class="diggit action">
            <span class="diggnum" id="digg_count">{{ article_obj.up_num }}</span>
        </div>
        <div class="buryit action">
            <span class="burynum" id="bury_count">{{ article_obj.down_num }}</span>
        </div>
        <div class="clear"></div>
        <div class="diggword"  id="digg_tips" style="color: red">
        </div>
    </div>
    {# 点赞点踩结束 #}
{% endblock %}

{% block js %}
  <script>
    $('.action').click(function (){
        let isUp= $(this).hasClass('diggit');
        let $div= $(this);
        $.ajax({
            url:'/up_or_down/',
            type: 'post',
            data:{
                'article_id':'{{ article_obj.pk }}',
                'is_up': isUp,
                'csrfmiddlewaretoken':'{{ csrf_token }}'
            },
            success:function (args) {
                if (args.code == 1000){
                    $('#digg_tips').text(args.msg)
                    //将数字加一
                    let oldNum = $div.children().text();
                    $div.children().text(Number(oldNum) + 1)
                }else{
                    $('#digg_tips').html(args.msg)
                }
            }
        })
    })
  </script>
{% endblock %}
```

```sh
import json
from django.db.models import F

def up_or_down(request):
    if request.is_ajax():
        back_dic = {'code':1000, 'msg':''}
        if request.user.is_authenticated():
            article_id = request.POST.get('article_id')
            is_up = request.POST.get('is_up')
            is_up = json.loads(is_up)
            print(is_up)

            #根据文章ID 查文章对象 根据对象查作者 和request。user比对
            article_obj = models.Article.objects.filter(pk=article_id).first()
            if not article_obj.blog.userinfo == request.user:
                is_click = models.UpAndDown.objects.filter(user=request.user,article=article_obj)
                if not is_click:
                    if is_up:
                        models.Article.objects.filter(pk=article_id).update(up_num=F('up_num') +1)
                        back_dic['msg'] = '点赞成功'
                    else:
                        models.Article.objects.filter(pk=article_id).update(down_num=F('down_num') + 1)
                        back_dic['msg'] = '点踩成功'
                    models.UpAndDown.objects.create(user=request.user,article=article_obj,us_up=is_up)
                else:
                    back_dic['code'] = '1001'
                    back_dic['msg'] = '已经点过了，不能再点'
            else:
                back_dic['code'] = '1002'
                back_dic['msg'] = '不要自己给自己点'
        else:
            back_dic['code'] = '1003'
            back_dic['msg'] = '请<a href="/login/">登录</a>'

        return JsonResponse(back_dic)
```



#### 评论

```sh
根评论：
     点击评论是里面内容清空
     渲染：
        临时渲染
        刷新页面渲染
        
子评论：

```

```sh
{% extends 'sitebase.html' %}

{% block css %}
    <style xmlns="http://www.w3.org/1999/html">
    #div_digg {
    float: right;
    margin-bottom: 10px;
    margin-right: 30px;
    font-size: 12px;
    width: 125px;
    text-align: center;
    margin-top: 10px;
}
    .diggit {
    float: left;
    width: 46px;
    height: 52px;
    background: url(/static/img/upup.gif) no-repeat;
    text-align: center;
    cursor: pointer;
    margin-top: 2px;
    padding-top: 5px;
}
    .buryit {
    float: right;
    margin-left: 20px;
    width: 46px;
    height: 52px;
    background: url(/static/img/downdown.gif) no-repeat;
    text-align: center;
    cursor: pointer;
    margin-top: 2px;
    padding-top: 5px;
}
    .clear {
    clear: both;
}
    </style>
{% endblock %}
{% block content %}

    <h1>{{ article_obj.title }}</h1>
    <div class="">
    {{ article_obj.content|safe }}
    </div>
    {# 点赞点踩开始 #}
    <div class="clearfix">
    <div id="div_digg">
        <div class="diggit action">
            <span class="diggnum" id="digg_count">{{ article_obj.up_num }}</span>
        </div>
        <div class="buryit action">
            <span class="burynum" id="bury_count">{{ article_obj.down_num }}</span>
        </div>
        <div class="clear"></div>
        <div class="diggword"  id="digg_tips" style="color: red">
        </div>
    </div>
    </div>
    {# 点赞点踩结束 #}

    {# 评论展示 #}
    <div>
    <ul class="list-group">
          {% for  comment in comment_list %}
                <li class="list-group-item">
                <span>#{{ forloop.counter }}楼</span>
                <span>{{ comment.comment_time|date:"Y-m-d h:i:s" }}</span>
                <span>{{ comment.user.username }}</span>
                <span><a  class="pull-right reply" username="{{ comment.user.username }}" comment_id="{{ comment.pk }}">回复</a></span>
                <div>
                    {{ comment.conent }}
                </div>
                </li>
          {% endfor %}
    </ul>
    </div>

    {# 文章评论开始 #}
    {% if request.user.is_authenticated %}

        <div>

            <p>发表评论</p>
            <div>
                <textarea name="comment" id="id_comment" cols="60" rows="10"></textarea>
            </div>
            <button class="btn btn-primary" id="id_submit">提交评论</button>
            <span style="color: red" id="error"></span>
        </div>
    {% else %}
        <li><a href="/register/">注册</a></li>
        <li><a href="/login/">登录</a></li>
    {% endif %}

    {# 文章评论结束 #}
{% endblock %}

{% block js %}
  <script>
    $('.action').click(function (){
        let isUp= $(this).hasClass('diggit');
        let $div= $(this);
        $.ajax({
            url:'/up_or_down/',
            type: 'post',
            data:{
                'article_id':'{{ article_obj.pk }}',
                'is_up': isUp,
                'csrfmiddlewaretoken':'{{ csrf_token }}'
            },
            success:function (args) {
                if (args.code == 1000){
                    $('#digg_tips').text(args.msg)
                    //将数字加一
                    let oldNum = $div.children().text();
                    $div.children().text(Number(oldNum) + 1)
                }else{
                    $('#digg_tips').html(args.msg)
                }
            }
        })
    })
    let parentId = null;
    $('#id_submit').click(function (){
        let conTent = $('#id_comment').val();
        $.ajax({
            url: '/comment/',
            type: 'post',
            data: {
                'article_id': '{{ article_obj.pk }}',
                'content': conTent,
                'parentId': parentId,
                'csrfmiddlewaretoken':'{{ csrf_token }}',
            },
            success:function (args){
                if (args.code == 1000){
                    $('#error').text(args.msg)

                    //清空评论看
                    $('#id_comment').val('');
                    let userName = '{{ request.user.username }}';
                    let temp = `
                    <li class="list-group-item">
                       <span>${userName}</span>
                       <span><a href="#" class="pull-right">回复</a></span>
                      <div>
                         ${conTent}
                        </div>
                    </li>
                    `
                    $('.list-group').append(temp);
                    parentId = null;

                }
            }
        })

    })

    $('.reply').click(function (){
         let commentUserName = $(this).attr('username');
         parentId = $(this).attr('comment_id');
         $('#id_comment').val('@'+ commentUserName + '\n').focus()


    })
  </script>
{% endblock %}
```

```sh
def comment(request):
    if request.is_ajax():
        back_dic = {'code': 1000, 'msg': ''}
        if request.method == 'POST':

            if request.user.is_authenticated():

                article_id = request.POST.get('article_id')
                content = request.POST.get('content')
                parent_id = request.POST.get('parent_id')
                with transaction.atomic():
                    models.Article.objects.filter(pk=article_id).update(comment_num=F('comment_num') + 1)
                    models.Comment.objects.create(user=request.user, article_id=article_id, conent=content, parent_id=parent_id)
                back_dic['msg'] = '评论成功'
            else:
                back_dic['code'] = '1001'
                back_dic['msg'] = '未登录'
            return JsonResponse(back_dic)
```



#### 后台管理

```sh
富文本编辑器

beautifulsoup4
```





# 项目二：权限管理



