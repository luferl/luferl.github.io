---
title: AntDesign Pro V5 到底怎么用之plugin-request
date: 2021-08-05 14:10:46
categories: 前端
tags: [React,前端]
---
&emsp;&emsp;AntDesign Pro V5中，使用了`@umijs/plugin-request`来实现请求的发送，这是在先前版本的request上进行了一次包裹而来的useRequest，使用起来更加清晰一些。

&emsp;&emsp;官网见：https://umijs.org/zh-CN/plugins/plugin-request

# 创建请求发起函数
&emsp;&emsp;为了使代码更便于阅读，还是将请求抽离成函数来实现。

&emsp;&emsp;与老版本并无不同，依然是在`src/services`下面来维护request请求的列表。如果使用了V5的脚手架，将会在`src/services`下面自动创建`ant-design-pro`和`swagger`两个文件夹，分别用于处理业务逻辑和生成接口swagger文档。

&emsp;&emsp;我们在`src/services/ant-design-pro`下的`api.js`中实现一个新的函数。
```js
export async function GetPersonIdentityBySearch(options) {
  return request('/api/fakeget', {
    method: 'POST',
    data: {options},
  });
}
```
# 请求调用
&emsp;&emsp;创建好发起函数之后，就可以在useRequest中进行调用，并实现传参。  
&emsp;&emsp;在`IdentityModelTest.js`中，我实现了一个手动触发的useRequest。关于IdentityModelTest是什么，可以参考另一篇文章:[AntDesign Pro V5 到底怎么用之plugin-model](https://coder.lufer.cc/%E5%89%8D%E7%AB%AF/AntDesign%20Pro%20V5%20%E5%88%B0%E5%BA%95%E6%80%8E%E4%B9%88%E7%94%A8%E4%B9%8Bplugin-model/)。
```js
import { useState, useCallback } from 'react'
//从api.js中引入我们创建的发起函数。
import { GetPersonIdentityBySearch } from '@/services/ant-design-pro/api';
//引入useRequest。
import { useRequest } from '@umijs/hooks';

export default function IdentityModelTest() {
  const [Identity,setIdentity] = useState(null);
  //实现一个手动触发的函数，可以通过run()来触发。
  const { loading, run } = useRequest(GetPersonIdentityBySearch,{
    manual: true,
    //在onSuccess中的result即可获取到返回值。
    onSuccess: (result, params) => {
      setIdentity(result);
    }
  });
  //根据官方说明文档，run()可以带参数，该参数将会传递到请求中。
  const searchIdentity = useCallback((conditions) => {
    run(conditions);
  }, [])

  return {
    Identity,
    searchIdentity,
  }
}
```
&emsp;&emsp;至此完成了在需要时的请求发起，参数传递，以及返回值处理。

# 其他请求
&emsp;&emsp;官方给出了一些直接使用useRequest发送请求的示例，但是这里要注意，如果系统检测到了第一个传入参数是字符串，将会直接发起请求，useRequest提供的其他接口例如manual，onSuccess，onError等都不会再生效，如果要使用这些API，一定要传入函数。
&emsp;&emsp;下面是几种官方示例写法。

```js
// 用法 1
const { data, error, loading } = useRequest('/api/userInfo');
​
// 用法 2
const { data, error, loading } = useRequest({
  url: '/api/changeUsername',
  method: 'post',
});
​
// 用法 3
const { data, error, loading, run } = useRequest((userId)=> `/api/userInfo/${userId}`);
​
// 用法 4
const { loading, run } = useRequest((username) => ({
  url: '/api/changeUsername',
  method: 'post',
  data: { username },
}));
```