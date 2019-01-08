# v-requset
> 突破小程序网络请求限制黑科技
> 让你更自由地请求任意网站数据

项目地址：[https://github.com/guren-cloud/v-request](https://github.com/guren-cloud/v-request)

## 简介
大家都知道，小程序的http网络请求是非常严格的：
1. 域名需要备案
2. 域名需要上https
3. 需要开发者在后台设置request白名单

**所以，这个项目出现了。**    
得益于小程序的云开发功能，让我们可以突破这个限制，来达到请求任何可访问的http数据！    
*（如：ip访问、http 80端口访问、自定义端口访问、未备案域名等场景）*

## 安装
### 部署云函数
项目分为两部分，一个是我们的小程序云函数代码，在`cloud`目录中。    
我们首先在开发者工具开通小程序云开发平台，然后初始化好环境之后，创建一个云函数，命名为：`v-request`：

![](https://box.kancloud.cn/72c94b4a4e755ed7aacad10d4ca15edd_596x378.png)

然后把`index.js`和`package.json`文件的内容替换为项目`cloud`目录中对应的文件内容，再右键进行上传部署（云端安装依赖）操作：

![](https://box.kancloud.cn/e6fab606b119b955d9765284ef66d8b0_928x439.png)


### 部署客户端
另一个文件，就是主目录下的`v-request.js`文件，这个是运行在我们小程序里的SDK客户端文件。    
我们把它放入小程序的目录，如`utils/`目录中，然后在`app.js`文件中进行`require`加载即可：

![](https://box.kancloud.cn/567a7a0d609527f5f6c34781d8c84d12_1193x620.png)

## 使用
通过上边的部署，我们已经可以在小程序的任意位置进行使用我们的`v-request`黑科技了！    
使用方法很简单，和[wx.request](https://developers.weixin.qq.com/miniprogram/dev/api/wx.request.html)官方API的用法基本保持一致    
我们只需要把原来的`wx.request`改成`wx.vrequest`即可。

### GET请求例子
```js    
wx.vrequest({
  url: 'https://mssnn.cn',
  success: ret => {
    console.log(ret.data);
  }
})
```
返回的数据：
![](https://box.kancloud.cn/6413d39b4f3ed0878f19097c54fd16d8_1398x611.png)

### POST请求例子
``` js
wx.login({
  success: ret => {
    wx.vrequest({
      url: 'https://wx5bbe79dd056cb238.mssnn.cn/v2/client/init',
      data: 'code=' + ret.code,
      dataType: 'json',
      method: 'POST',
      header: {
        'Content-Type': 'application/x-www-form-urlencoded'
          },
      success: res => {
        console.log('[post.res]', res);
      }
    })
  }
})
```
返回的数据：
![](https://box.kancloud.cn/b9f81ed3207972f0c508ded7bd1a97d4_1281x818.png)

## 其他说明
代码仅供学习，请勿滥用或用于非法用途。    
本方法由[古人云小程序](https://mssnn.cn)原创研发    
欢迎你关注我们学习更多小程序开发技巧！

![](https://mssnn.cn/img/qr_gurenyun.jpg)
