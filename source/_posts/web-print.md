title: 关于web端打印CSS技巧
date: 2018-01-26 17:18:28
tags: [technology,css]
---

之前做健康管理系统时候，调查了很久的web打印，纯粹的css来控制打印样式实际效果并不理想，对于简单的页面实现尚可，复杂的例如需要设置页眉页脚、页数等的就无可奈何了，只能借助一些第三方插件jsPDF之类。
下面简单描述下CSS可以控制的内容：

**1、针对打印的样式，而不是屏幕显示样式**
针对打印做的一些特殊样式，可以使用css的媒体查询来实现：
```
@media print {
    body { 
        color: #000; background: #fff; 
    }
}
```

**2、保证不被跨页打印**
使用page-break-after属性可以避免在元素后插入分页符：
```
h2, h3 { 
    page-break-after: avoid; 
}
```

**3、确保某内容，在新的一页开始**
使用page-break-before属性可以控制某些元素打印的时候一定会在新的一页开始：
```
article {
    page-break-before: always;
}
```

**4、确保某内容，在新的一页开始**
使用page-break-inside属性可以控制某些元素打印的时候不会被分页，亲测chrome中效果较好：
```
ul, img {
    page-break-inside: avoid;
}
```

**5、背景图片和颜色**
需要打印背景和图片时（彩色打印），需要添加如下媒体查询样式，该样式chrome支持较好：
```
@media print {
    * {
        -webkit-print-color-adjust: exact;
        print-color-adjust: exact;
    }
}
```

以上目前开发中遇到的可以做优化的，推荐chrome浏览器效果较好，但是整体还是有点弱哎。