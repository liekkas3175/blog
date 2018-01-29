title: 微信公众号开发填过的坑
date: 2016-11-30 15:39:48
tags: technology
---

[前言]本次微信公众号webapp前端框架为vue，基于 vue-cli 脚手架生成项目模板，加入了 vue-router ，vuex 等配套设施，UI和组件库使用了[vux](https://github.com/airyland/vux "vux")。

PS：忍不住还是想吐槽下腾讯自己在安卓上内置的X5内核的浏览器，果然不负移动端IE6的称谓，一堆不一致的地方，而且同等情况性能比其他浏览器要差好多。

<br />**1、微信支付授权目录**
项目为单页应用，引入了vue-router做路由管理，使用hashbang模式即路由模式为：`http://example.com/#!/sub/index` 的形式。
微信支付允许配置3个目录为授权目录，另外允许配置一个测试环境目录，授权目录必须配置到最后一级目录，配置在根目录不行。到这里其实还都不是问题，问题是微信判断当前路径的方式。
经尝试，微信IOS和安卓内置浏览器对这种hashbang模式路由解析不一致，所以通常配置一个授权目录会发现在不同版本手机上总有遇到提示“URL未注册”，然而它只允许配置三个路由，如果有两个页面需要使用支付就会出现问题了。
解决方案：
1）支付统一跳转到一个页面中转
2）`http://example.com/?#!/sub/index`，微信浏览器会把井号“#”后面的内容给去掉，授权目录只需要配置为`http://example.com/`即可。

<br />**2、用document.title=“xxx”动态修改title，在ios的微信下面不生效的hack**
```javascript
document.title = 'title';
let $iframe = document.createElement("iframe");
$iframe.src = 'static/favicon.ico';
document.body.appendChild($iframe); 
$iframe.onload = function(){
    setTimeout(function() {
        let pNode = $iframe.parentNode;
        if(pNode){pNode.removeChild($iframe);}
    }, 0)
};
```
<br />**3、判断微信内置浏览器的方法**
```javascript
if(/MicroMessenger/i.test(navigator.userAgent)){
    alert("当前微信内置浏览器")
}
```

<br />**4、安卓手机上对CSS3部分内容支持不行，flex布局需要注意**


