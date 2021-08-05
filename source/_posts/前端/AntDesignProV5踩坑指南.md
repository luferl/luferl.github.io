---
title: AntDesign Pro V5 踩坑指南
date: 2021-07-30 16:37:50
categories: 前端
tags: [React,前端]
---
&emsp;&emsp;最近又在写前端了，掏出了祖传的AntD，发现已经更新到5.0版本了，而且通过umi安装的话是选不了老版本的。  
&emsp;&emsp;新版本怎么说呢，用起来真是坑坑洼洼的，而且官网文档写的一言难尽，有些东西他写了，但又没完全写，你看懂了，但又没完全看懂。  
&emsp;&emsp;记录一下V5版本和旧版本的一些不同之处。
# 全局化配置
## 样式配置与快速生成
&emsp;&emsp;V5版本把全局化配置抽离出来，放在了`\config\defaultSettings.js`文件下,可以通过`https://preview.pro.ant.design`右侧的齿轮快速的生成配置Json，然后放到`defaultSettings.js`里面。
## 去掉全球化与修改页脚
&emsp;&emsp;我这小项目估计也没有外国人看了，关掉全球化省的控制台一直报Warning。
```js
//config\config.js
layout: {
    locale: false,   //locale改为false
    siderWidth: 208,
    ...defaultSettings,
  },
```
&emsp;&emsp;页脚在Footer里面，改成自己的公司名。
```js
//src\components\Footer\index.jsx
import { useIntl } from 'umi';
import { GithubOutlined } from '@ant-design/icons';
import { DefaultFooter } from '@ant-design/pro-layout';
export default () => {
  const intl = useIntl();
  // const defaultMessage = intl.formatMessage({
  //   id: 'app.copyright.produced',
  //   defaultMessage: '蚂蚁集团体验技术部出品',
  // });
  return (
    <DefaultFooter
      copyright={`2021 - 中国烟草总公司云南省公司`}
      links={[
        {
          // key: 'Ant Design Pro',
          // title: 'Ant Design Pro',
          // href: 'https://pro.ant.design',
          // blankTarget: true,
        },
      ]}
    />
  );
};
```
# 菜单与路由
&emsp;&emsp;我记得V2的时候还要在`src\commom\`下面写`menu.js`和`routes.js`。  
&emsp;&emsp;在V4的时候已经抽离到了`config\config.js`里面。  
&emsp;&emsp;这次的V5将routes.js提取包装成独立文件，然后再config.js里面引用了。这样确实好一些，不然config.js就太乱了。
```js
//config\config.js
import routes from './routes';
  ......
// umi routes: https://umijs.org/docs/routing
  routes,
```
&emsp;&emsp;这里我脑瘫了一次，我在routes里面写子菜单的时候，没给父级菜单写path，结果导致了一个很牛的BUG，就是所有的菜单只有第一个嵌套子菜单可以显示，再往下的菜单点了之后一个页面都加载不出来，而在这项之前的菜单不受影响。  
&emsp;&emsp;正确写法：
```js
//config\routes.js
{
    name: '主体管理',
    icon: 'table',
    path:'/Identity',
    access:'canAdmin',
    routes:[
      {
        name: '自然人主体管理',
        icon: 'table',
        path: '/Identity/Person',
        component: './Admin/Identity/IdentityofPerson',
      },
      {
        name: '组织机构主体管理',
        icon: 'table',
        path: '/Identity/Org',
        component: './Admin/Identity/IdentityofOrg',
      },
    ]
  },
```
# 菜单与路由的权限设置
&emsp;&emsp;在老版本中，路由权限是在routes下面写authority来实现的，贴一个老的例子。
```js
routes: [
    {
        path: '/',
        component: '../layouts/BasicLayout',
        authority: ['admin', 'user'],  //通过authority设置可访问的用户类别。
        routes: [
        {
            path: '/',
            redirect: '/user/login',
        },
        {
            path: '/welcome',
            name: 'welcome',
            icon: 'smile',
            component: './Welcome',
        },
......
```
&emsp;&emsp;在V5中，官方使用了`@umijs/plugin-access`来实现权限控制，老的`Authority.js`组件也已经被删掉了。官方文档见`https://pro.ant.design/zh-CN/docs/authority-management`。  

&emsp;&emsp;首先修改access.js，添加一个我们自己的鉴权逻辑。
```js
//src\access.js
/**
 * @see https://umijs.org/zh-CN/plugins/plugin-access
 * */
export default function access(initialState) {
  const { currentUser } = initialState || {};
  return {
    canAdmin: currentUser && currentUser.access === 'admin',
     //这里是返回的用户数据里面有一个access字段，通过是admin还是user来表示用户权限，所以添加了一个canUser的promise，检查用户权限组是否为user。
    canUser:currentUser && currentUser.access === 'user' 
  };
}
```
&emsp;&emsp;然后只需要在`routes.js`里面设置`access`需要调用的promise即可。
```js
//config\routes/js
{
    name: '主体管理',
    icon: 'table',
    path:'/Identity',
    access:'canAdmin',          //调用canAdmin来检查是否符合管理员权限
    routes:[
        ......
    ]
  },
  {
    name: '个人中心',
    icon: 'table',
    access:'canUser',           //调用canUser来检查是否符合用户权限。
    path: '/Account',  
    component: './user/AccountManage',
  },
```

## 路由逻辑
routes.js应该是一个自上而下的逐个适配过程，当找到能匹配的规则时就执行跳转，不再向下执行，所以通配符一定要放在最后面。
```js
  //前面都不匹配，检查/
  {
    path: '/',
    redirect: '/index',
  },
  //所有的都没有匹配，跳转404
  {
    component: './404',
  },
];
```

# 手动操作表单内容
&emsp;&emsp;如果要取一个Form里面各项内容的值，需要创建一个formInstance，和form绑定之后就可以取值。
```js
export default ()=>{
  const [formRefofModal]=Form.useForm();   //创建一个formInstance
  ......
  function(){
      //在需要的地方通过formRef.current.getFieldsValue来取值
      const values=formRefofModal.getFieldsValue(true);
      console.log(values);
      //通过formRef.current.resetFields来快速重置表单项。
      formRefofModal.resetFields();
  }
  ......
  render(){
      ......
        // 通过form属性绑定到创建的ref
         <Form layout="vertical" hideRequiredMark form={formRefofModal}> 
            ......
      ......
  }


//console输出的表单值
{
    "Name": "张三2222",
    "PhoneticDisplayName": "zhangsan3333",
    "Sex": "1",
    "Ethnicity": "汉族",
    "Mobile": "123123123123",
    "Email": "123123",
    "ChineseIDCard": "1231231"
}
```
# 使用区块
&emsp;&emsp;AntDesign预先封装了一些组件模板，起名叫做`区块`，通过引入区块通过简单修改快速的实现页面。

&emsp;&emsp;但是这个区块想用起来可真TM费事!!

&emsp;&emsp;首先是官方文档里面对于区块的介绍。  
&emsp;&emsp;https://pro.ant.design/zh-CN/docs/assets/  
&emsp;&emsp;光介绍了什么是区块，怎么用区块，但是没告诉你都有什么区块，也没给你链接。

&emsp;&emsp;最后还是在github上面找到了全部的区块库。  
&emsp;&emsp;https://github.com/ant-design/pro-blocks

&emsp;&emsp;随便点进去一个区块，readme里面写了个命令教你怎么安装。

![区块readme](https://pic.lufer.cc/images/2021/08/03/image.png)

&emsp;&emsp;你以为你用这个命令能装上？Navie，直接给你一个报错，让你当场懵逼。

![报错](https://pic.lufer.cc/images/2021/08/03/image380b55601b8c34b5.png)

&emsp;&emsp;最后搜到了一个issue，https://github.com/ant-design/ant-design-pro/issues/4534

&emsp;&emsp;这个issue下面有一个开发者说了一句话：

![开发者回复](https://pic.lufer.cc/images/2021/08/03/imagec6eeffa7aa285503.png)

&emsp;&emsp;你以为你把命令改成`umi block add AccountSettings`就行了？Naive，会报跟先前一样的错。

&emsp;&emsp;最后还是这个提问的人提供了一个解决办法。

>后续：经过测试，使用umi block add https://github.com/ant-design/pro-blocks/tree/master/UserLogin可以正常安装。

&emsp;&emsp;于是我把命令改成了`umi block add https://github.com/ant-design/pro-blocks/tree/master/AccountSettings`，安装成功。

安装成功之后页面起不来，控制台报错：
![缺少组件](https://pic.lufer.cc/images/2021/08/03/image30e044d1c08dfac3.png)

&emsp;&emsp;试图删掉node_modules重新`npm install`结果项目整个起不来了，最后还是特么重新建的项目，不想整这个区块了，还不如自己写。

&emsp;&emsp;服了。

&emsp;&emsp;未完待续，边填坑边记录。

