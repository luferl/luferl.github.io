---
title: 使用Python读取xlsx文件内容并操作LDAP
date: 2021-09-18 12:32:10
tags: [Python]
categories: Python
---
&emsp;&emsp;最近手上一个项目要用LDAP中的行政区划代码做校验，但是目前搭建的LDAP中行政区划代码太老。  
&emsp;&emsp;同事从网上扒了2020年国家统计局的行政区划代码，以xlsx文件形式存储，要读取其中内容并更新LDAP中的区划名称，不存在的要新增。

# 启用简单身份验证
&emsp;&emsp;目前的LDAP用的是Kerberos验证，测试了python-ldap和ldap3两个库，都没弄明白怎么实现这种验证方式，最后还是用了简单身份验证。

&emsp;&emsp;先找个目录创建一个用户。

&emsp;&emsp;`新建-对象`，类选择`user`，填写用户名，我这里创建了一个`testuser`。

![新建用户](https://pic.lufer.cc/images/2021/09/24/image.png)

&emsp;&emsp;然后在创建好的用户上`右键-重置密码`，设置一个密码。

&emsp;&emsp;默认的账户是禁用的，要先启用。`右键-属性`，找到`MsDS-UserAccountDisabled`，设置为`未设置`或`禁用`。

&emsp;&emsp;然后将账户添加到管理员中，找到`CN=Roles`,修改`CN=Administrators`的属性，找到`member`。

&emsp;&emsp;选择`添加DN`，把刚刚创建的用户DN（distinguishedName）添加进去，例如`CN=testuser,DC=tobaccoid,DC=com`

![添加到管理员列表](https://pic.lufer.cc/images/2021/09/24/imageb87c894861b52aaf.png)

&emsp;&emsp;至此就可以用这个用户名和密码进行简单身份验证登录了。

# 安装xlrd
&emsp;&emsp;要读取excel文件，需要用到xlrd这个库，但是要注意在1.2.0版本之后就不支持xlsx文件了，因此要安装指定版本
`pip install xlrd==1.2.0`

&emsp;&emsp;装好之后就可以进行读取，基本用法如下：
```python
import xlrd
# 读取文件
wb = xlrd.open_workbook('data.xlsx')
# 获取工作表
table = data.sheets()[0]          #通过索引顺序获取
table = data.sheet_by_index(sheet_indx)) #通过索引顺序获取
table = data.sheet_by_name(sheet_name)#通过名称获取
# 获取数据范围
nrows = table.nrows   #获取有效行数
ncols = table.ncols   #获取有效列数
# 行操作
table.row(rowx)  #返回由该行中所有的单元格对象组成的列表
table.row_slice(rowx)  #返回由该列中所有的单元格对象组成的列表
table.row_types(rowx, start_colx=0, end_colx=None)    #返回由该行中所有单元格的数据类型组成的列表
table.row_values(rowx, start_colx=0, end_colx=None)   #返回由该行中所有单元格的数据组成的列表
table.row_len(rowx) #返回该列的有效单元格长度
# 列操作
table.col(colx, start_rowx=0, end_rowx=None)  #返回由该列中所有的单元格对象组成的列表
table.col_slice(colx, start_rowx=0, end_rowx=None)  #返回由该列中所有的单元格对象组成的列表
table.col_types(colx, start_rowx=0, end_rowx=None)    #返回由该列中所有单元格的数据类型组成的列表
table.col_values(colx, start_rowx=0, end_rowx=None)   #返回由该列中所有单元格的数据组成的列表
# 单元格操作
id = table.cell(row,col).value  #获取row行col列的单元格的值
```
# 安装ldap3
&emsp;&emsp;python-ladp这个库有点老了，最后用了ldap3这个库进行操作:`pip install ldap3`。  
&emsp;&emsp;官方文档：https://ldap3.readthedocs.io/

&emsp;&emsp;装好之后基本操作如下：
```python
from ldap3 import Server, Connection, ALL, SUBTREE, MODIFY_REPLACE
# 连接服务器
s = Server('serveraddress', get_info=ALL)  
# 指定使用的用户
c = Connection(s, user='CN=testuser,DC=tobaccoid,DC=com', password='password')
# 建立连接
c.bind()
# 检索操作
## search_base：要检索的根目录
## search_filter：过滤器，设定检索条件，例如这里是指定属性cn为特定值，且类型为locality。
## attributes：需要返回的属性，例如这里返回的内容中就带有属性cn和l
filter = '(&(cn=' + oldcode + ')(objectClass=locality))'
c.search(search_base='C=CN,DC=tobaccoid,DC=com', search_filter=filter, search_scope=SUBTREE, attributes=['cn', 'l'])
# 返回值在c.entries中，是一个列表，列表中的数据是json字符串，先转为对象
tempentry=c.entries[0].entry_to_json()
entry=json.loads(tempentry)
# 更新属性
## 更新属性需要用dn作为主键，因此需要得到dn，再更改属性，此处更改了cn这个属性的值为newcode
olddn = entry['dn']
c.modify(olddn,{'cn': [(MODIFY_REPLACE, [newcode])]})
# 更新DN
## 如果要更改DN，需要运动modify_dn这个值，且此操作不能更新其他属性。
c.modify_dn(olddn, 'L='+name)
# 新增操作
## add操作可以同时创建新的DN，并赋予其属性值，这里将新增的条目objectclass设置为locality，属性cn设置为newcode。
c.add(newdn,['locality'],{'cn':newcode})
```
# 完整代码
&emsp;&emsp;因为我这里的xlsx文件和实际情况有些区别，因此先做了一次数据处理。
```python
from ldap3 import Server, Connection, ALL, SUBTREE, MODIFY_REPLACE
import json
import xlrd
# 处理工作表
wb = xlrd.open_workbook('data.xlsx')
# 按工作簿定位工作表
sh = wb.sheet_by_name('tab_citys')
total = sh.nrows
result = []
head = "C=CN,DC=tobaccoid,DC=com"
for i in range(1, total):
    id = sh.cell(i, 0).value  # id
    parid = sh.cell(i, 1).value  # parent_id
    name = sh.cell(i, 2).value  # city_name
    oldcode = sh.cell(i, 5).value  # city_code
    newcode = sh.cell(i, 6).value  # code
    temp = {}
    if parid == 0:
        temp['id'] = id
        temp['dn'] = "L=" + name + "," + head
        temp['name'] = name
        temp['oldcode'] = oldcode
        temp['newcode'] = newcode
        result.append(temp)
        print(temp)
    else:
        for city in result:
            if city['id'] == parid:
                temp['id'] = id
                temp['dn'] = "L=" + name + "," + city['dn']
                temp['name'] = name
                temp['oldcode'] = oldcode
                temp['newcode'] = newcode
                result.append(temp)
                print(temp)
# 连接服务器
s = Server('serveraddress', get_info=ALL)  # define an unsecure LDAP server, requesting info on DSE and schema
# define the connection
c = Connection(s, user='CN=username,DC=tobaccoid,DC=com', password='password#')
c.bind()
# 遍历更新
for city in result:
    oldcode = city['oldcode']
    newcode = city['newcode']
    newdn=city['dn']
    filter = '(&(cn=' + oldcode + ')(objectClass=locality))'
    c.search(search_base='C=CN,DC=tobaccoid,DC=com', search_filter=filter, search_scope=SUBTREE, attributes=['cn', 'l'])
    res = len(c.response)
    if res > 0:
        tempentry=c.entries[0].entry_to_json()
        entry=json.loads(tempentry)
        print(entry)
        olddn = entry['dn']
        name = city['name']
        #修改code
        c.modify(olddn,{'cn': [(MODIFY_REPLACE, [newcode])]})
        if(olddn!=newdn):
            #修改name
            c.modify_dn(olddn, 'L='+name)
            print("update:"+olddn)
    else:
        c.add(newdn,['locality'],{'cn':newcode})
        print("add:" + newdn)
```

