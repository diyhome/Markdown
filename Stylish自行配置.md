---
title: Stylish自行配置
tags: 配置,技巧
grammar_cjkRuby: true
---


## 简介
Stylish是浏览器的一个样式表扩展，支持主流的浏览器`Chrome`以及`Firefox`,听说`360`也支持
这个扩展可以帮助你重定义网页的[CSS][1]样式表
>觉得网页丑
网页对自己的终端适配不够好
And so on...

没关系,Stylish都可以帮你解决

## 使用前的准备
What?使用还要准备?的确,你需要找到你这个网页所需要的[CSS][2]样式表,你可以右击Stylish选择[查找适合此网站的样式表][3]
或者,你可以自己写一份(这是本篇文章的主要部分)
自己写的话浏览器要有开发者工具,例如`Firebug`

## Do it yourself
### 应用实例-广告屏蔽
一直以来广告都是最为头疼的东西,特别是那些容易误点击的广告.其实对于网页而言,广告也是网页的一种`元素`,既然是网页的一部分就可以用[CSS][4]规则去定义它,譬如你可以使用`display:none`将其隐藏,具体方法如下:
进入你想重定义[CSS][5]的网站(这里以[笔趣阁][6]为例,按`F12`打开开发者工具,选择如图所示按钮查找到你需要屏蔽`元素`的`ID`或者`class`值并记录
`小贴士:你可以尝试往上找几层,把这个框给选中,注意别选中其它的就好了.`
![选择Firebug元素定位器][7]
![详细指导][8]
可以明显的看到当我把鼠标对到顶层元素的时候那一栏都变成选中了
![选中][9]
然后在`Stylish`图标上面右击,`新建样式`->`提供给*****`,如图
![新建样式][10]
在如图所示位置开始编写你希望的CSS样式,这里我是要屏蔽下面那个推荐的,代码是`#hm_t_24623{display: none}`
>这里补充一下,ID的话前面要加上特殊字符`#`,class要加上`.`,就和这个例子所使用的是ID一样

`别忘记了对这个样式表命名并且保存,保存后查看原始网页`
![code][11]
好的我们现在可以查看下原来的网页,发现那个一栏推荐书单是没了,但是还有些不和谐的元素在里面,我们可以一一将其除去
![除去][12]
还是按照之前的方法找出这些样式的`ID`或者`class`并且一一除去
![除去其它][13]
>这里有一个小技巧(其实也是偷懒).当我们要对不同的元素做同样的工作的时候(这里是需要写:display:none),我们可以在前一个元素后面加一个`,`,如图,这样可以批量帮助我们完成

![批量][14]
到这里,广告屏蔽的教程就完成了.其实也很简单,就是利用了[CSS][15]的属性`display:none`
### 应用实例-网站拓宽
如果你看到这里还滋滋有味,那么我很荣幸.
下面我会给大家介绍一下怎么拓宽网页
>为什么我们要拓宽网页?
>现在大部分网页的布局都适应了低分辨率,可是当用高分辨率的设备进行阅读的时候就会出现网页不够大,或者像教程中这个例子[笔趣阁][16]一样是小说网站但是阅读样式让你很不舒服

工具还是和之前一样并未有什么变化,同样的你也要找到你需要更改的元素的ID或者class值
![选择][17]
我们很快的选择并发现了的确是有限制宽度的属性`width=976px;`,并且将其改为`auto`
>小贴士:拓宽什么的最好不要直接去Stylish里面写,现在Firebug之类的工具里面改改看看效果

![修改][18]
修改完成后我们并未发现网页变大了,怎么回事呢?
![然并卵][19]
我们可以向上找一级发现这个元素还有一个父级对象,定位到这个父级对象查看果然还有我们未曾注意到的一个宽度定义`width=980px;`
![重新修改][20]

这里我们重新修改为`80%`,为什么不使用`100%`?网页的两边总该要留一点空间不然对于密集恐惧症来说就太难受了
![拓宽完成][21]
到了这里拓宽工作就做完了,还记得我们刚刚干了些什么吗?把刚刚修改的东西往新建的样式表里面写就好了,代码如下:
```
  /*拓宽*/
  .box_con{width: auto}
  .content_read{width: 80%}
```
### 一些善后工作
到了这里我们的工作就快要完成了,但是这个样式表还是有点不足的,这里需要对其进行细微的调整
![缺陷][22]
![缺陷][23]
![缺陷][24]
可以看到有些元素没有居中对齐,还有就是图2的东西我们不需要了以及背景颜色的修改
还是老套路,CSS选择修改
最后修改完成后的样式如下:
![成功][25]
还有一些小细节优化就待你们自己去咯,主要是懒
```
@namespace url(http://www.w3.org/1999/xhtml);

@-moz-document domain("www.biquge.com") {
  /*屏蔽*/
  #hm_t_24623,.con_title,.footer_link,.footer_cont,#bdshare,.lm,.bottem1,#page_set,.ywtop{display: none}
  
  /*拓宽*/
  .box_con{
    width: auto;
    border: none;
  }
  .content_read{width: 80%}
  
  /*后期*/
  .bottem2{
    margin: auto !important;
    border-top:black;
  }
  body,.con_top{
    background-color: #f1e5c9 !important;
    border-bottom:none;
  }
  .nav{
    background:#f1e5c9 !important
  }
  .bookname{border-bottom:none !important;}
  
  .nav a{
    color: #000 !important;
  }
  
  .header_search button{background:#f2ebc9 }
  
}
```
## 结尾
最后要说的就是如果有一些无法修改的情况可以试试在属性后面加上`!important`
还有就是最好用ID屏蔽,class可能会误伤
这个只是一个最浅显的例子,类似抛砖引玉


  [1]: https://zh.wikipedia.org/wiki/%E5%B1%82%E5%8F%A0%E6%A0%B7%E5%BC%8F%E8%A1%A8
  [2]: https://zh.wikipedia.org/wiki/%E5%B1%82%E5%8F%A0%E6%A0%B7%E5%BC%8F%E8%A1%A8
  [3]:https://userstyles.org/
  [4]: https://zh.wikipedia.org/wiki/%E5%B1%82%E5%8F%A0%E6%A0%B7%E5%BC%8F%E8%A1%A8
  [5]: https://zh.wikipedia.org/wiki/%E5%B1%82%E5%8F%A0%E6%A0%B7%E5%BC%8F%E8%A1%A8
  [6]:http://www.biquge.com/0_147/2514088.htmlhttp://www.biquge.com/0_147/2514088.html
  [7]: http://ofyep4zkc.bkt.clouddn.com/1.png "1.png"
  [8]: http://ofyep4zkc.bkt.clouddn.com/2.png "2.png"
  [9]: http://ofyep4zkc.bkt.clouddn.com/3.png "3.png"
  [10]: http://ofyep4zkc.bkt.clouddn.com/Stylishdiy-1.png "Stylishdiy-1.png"
  [11]: http://ofyep4zkc.bkt.clouddn.com/stylishhtlp-2.png "stylishhtlp-2.png"
  [12]: http://ofyep4zkc.bkt.clouddn.com/stylishhtlp-3.png "stylishhtlp-3.png"
  [13]: http://ofyep4zkc.bkt.clouddn.com/stylishhtlp-4.png "stylishhtlp-4.png"
  [14]: http://ofyep4zkc.bkt.clouddn.com/stylishhtlp-5.png "stylishhtlp-5.png"
  [15]: https://zh.wikipedia.org/wiki/%E5%B1%82%E5%8F%A0%E6%A0%B7%E5%BC%8F%E8%A1%A8
  [16]:http://www.biquge.com/0_147/2514088.htmlhttp://www.biquge.com/0_147/2514088.html
  [17]: http://ofyep4zkc.bkt.clouddn.com/stylishhtlp-7.png "stylishhtlp-7.png"
  [18]: http://ofyep4zkc.bkt.clouddn.com/stylishhtlp-6.png "stylishhtlp-6.png"
  [19]: http://ofyep4zkc.bkt.clouddn.com/stylishhtlp-8.png "stylishhtlp-8.png"
  [20]: http://ofyep4zkc.bkt.clouddn.com/stylishhtlp-9.png "stylishhtlp-9.png"
  [21]: http://ofyep4zkc.bkt.clouddn.com/stylishhtlp-10.png "stylishhtlp-10.png"
  [22]: http://ofyep4zkc.bkt.clouddn.com/stylish-bug-1.png "stylish-bug-1.png"
  [23]: http://ofyep4zkc.bkt.clouddn.com/stylishhtlp-11.png "stylishhtlp-11.png"
  [24]: http://ofyep4zkc.bkt.clouddn.com/stylishhtlp-12.png "stylishhtlp-12.png"
  [25]: http://ofyep4zkc.bkt.clouddn.com/stylishhtlp-13.png "stylishhtlp-13.png"