---
title: CSS 浮动应用 
tags: 新建,模板,小书匠
grammar_cjkRuby: true
---


应网友之邀仿写了一个网站的一小部分，代码较简单，就是`CSS`的`float`属性的应用
下面这个是被仿写网站的样式:http://www.blypay.cn/
![enter description here][1]
## 代码
可以通过源代码不难发现这一块的源码其实不复杂,鉴于源码过于繁琐,这里列出我简化后的代码
```
<h2 class="title">我们的服务</h2>
<div id="demo_main">
<div class="demo_left">
  <div>
    <h3 class="demo_h3">安全保证</h3>
    <img src="logo.png" />
    <p class="demo_p">实时查询，安全可靠，多重账号保护措施安全可靠； 业内费率比率高，维护商户利益，7*24小时全天候服务；</p>
  </div>
  <div class="demo_logo">
    <h3 class="demo_h3">资金回笼</h3>
    <img src="logo.png" />
    <p class="demo_p" >一次轻松接入所有支付，省时省心省力， 结算费率低，利润高！</p>
  </div>
</div>
<div class="demo_right">
  <div>
    <h3 class="demo_h3">我们优势</h3>
    <img src="logo.png" />
    <p class="demo_p">对接费率超低，比其它平台更便宜.24小时监视订单 和资金安全，国际认证SSL 全程安全无忧！</p>
  </div>
  <div>
    <h3 class="demo_h3">高效服务</h3>
    <img src="logo.png" />
    <p class="demo_p">我们提供7X24小时在线服务，对日交易高额用户可提供一对一服务！</p>
  </div>
  </div>
</div>
```
>其中的logo.png是我杜撰的，因为我在原始网页哪里没有找到这个资源，只有一个\<i>的伪标签
>所以在这里我用logo.png代替了这四个logo

这就是这个网页的具体模型,也可以称其为骨架

![enter description here][2]
## 思路
原始的是左右对称的一个2x2的布局,所以我就想到了`浮动`,刚好一个`左浮动`一个`右浮动`
我们令一个`<H2>`一个`<img>`一个`<p>`为一组(即源码中未命名的`div`),这样我们就有四组元素
每两组又为一层,即源码中的`demo_right`和`demo_left`
为其添加`float`属性,一个`左浮动`一个`右浮动`
为了防止浮动之后会互相占位置我们为`demo_left`&`demo_right`限定宽度为`500px`
```
.demo_left {
	width: 500px;
	float: left;
}
.demo_right {
	width: 500px;
	float: right;
}
```

---
添加完毕后可以看到如我们所想的那样左右浮动了,但是,似乎标题和内容以及图片的位置不对诶

![enter description here][3]

我们应该把标题以及文字向左移,并且标题要下沉
这里考虑到四个块的标题和文字的位置都是一样的,所以令其共用一个类名:`demo_h3`以及`demo_p`
令`demo_h3`向右浮动,发现标题跑到过于右边去了,于是用外边距予以修正,顺便修正了下`demo_p`

### 修正代码
```
.demo_h3 {
	float: right;
	margin-right: 340px;
	margin-top: 0px;
}
.demo_p {
	margin-left: 75px;
	margin-top: -30px;

}
```
用`text-align: center;`将标题居中,这时我们的网页就像这样了

![enter description here][4]

发现中间空的行距太大了.所以加上一个`div`标签嵌套住`demo_left`&`demo_right`
就是那个class为`demo_main`
使其居中并且限制宽度为`1200px`,1200-500\*2=200,也就是中间空出200像素来
```
.#demo_main {
	margin: 0 auto;
	width: 1200px;
}
```
![enter description here][5]
成品,只需要小小的修改下颜色以及主字体样式就好了

## 心得
用HTML去写好一个网页的框架,辅以CSS修饰
还有就是尽量考虑适应新的布局,方便修改以及维护,如我在文中使用的浮动,最后调整两个浮动中间宽度的时候只需要嵌套一个`div`即可

---
相应的代码以上传,欢迎下载
[Github][6]


  [1]: http://ofyep4zkc.bkt.clouddn.com/QQ20170702004225.png "QQ20170702004225.png"
  [2]: http://ofyep4zkc.bkt.clouddn.com/QQ20170702005240.png "QQ20170702005240.png"
  [3]: http://ofyep4zkc.bkt.clouddn.com/QQ20170702011202.png "QQ20170702011202.png"
  [4]: http://ofyep4zkc.bkt.clouddn.com/QQ20170702012539.png
  [5]: http://ofyep4zkc.bkt.clouddn.com/QQ20170702013351.png "QQ20170702013351.png"
  [6]: https://github.com/diyhome/HTML-CSS_float