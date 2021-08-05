---
title: AntDesign Pro V5 到底怎么用之plugin-model
date: 2021-08-05 10:26:22
categories: 前端
tags: [React,前端]
---
&emsp;&emsp;在AntDesign Pro v5中，抛弃了先前的`Dva`,不再使用原先的数据流方案，而是使用了`@umijs/plugin-model`。

&emsp;&emsp;官方网址见：https://umijs.org/zh-CN/plugins/plugin-model

# 创建Model
&emsp;&emsp;在`src/models`下面创建model文件，按照官方的说法，只要创建的model符合hooks model的规范，就可以自动检测到，文件名则对应最终 model 的 name。  
&emsp;&emsp;这里我们新建一个叫做`IdentityModelTest.js`的文件。
```js
import { useState, useCallback } from 'react'
//这是我自己写的一个request请求函数，具体可见另一篇关于useRequest的介绍。
import { GetPersonIdentityBySearch } from '@/services/ant-design-pro/api';
import { useRequest } from '@umijs/hooks';

export default function IdentityModelTest() {
  //创建一个名为Identity的State，并配套一个setIdentity的方法用于更新State。
  const [Identity,setIdentity] = useState(null);
  //这是一个发起请求的手动触发函数，并在成功后通过setIdentity更新了State。
  const { loading, run } = useRequest(GetPersonIdentityBySearch,{
    manual: true,
    onSuccess: (result, params) => {
      setIdentity(result);
    }
  });
  //定义一个方法searchIdentity，并传入参数conditions。
  const searchIdentity = useCallback((conditions) => {
    run(conditions);
  }, [])
  //决定了向外暴露的值和方法。
  return {
    Identity,
    searchIdentity,
  }
}
```
&emsp;&emsp;其实这个model和Dva时期的model功能上来讲都差不多，定义state，通过操作更改state，只不过把fetch和reducer改成了useRequest和setState。
# 使用Model
&emsp;&emsp;有了Model之后，就可以在具体的业务场景中进行消费使用，并且在model的state更新之后，也会同步触发页面的更新。
```js
//引入useModel才能使用model
import { useModel } from 'umi';
export default () => {
    //通过useModel('Model名')来使用Model，并解构其暴露出来的值或方法。
    const { Identity,searchIdentity} = useModel('IdentityModelTest');  
    //此时就可以通过暴露出来的接口传参并执行相关的业务逻辑。
    searchIdentity(value);
    //Identity也可以直接使用。
```