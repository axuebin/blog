---
layout: post
title:  "百度Web前端技术学院-三栏式布局"
date:   2016-03-15 14:12:00
categories: 前端
tags: Html Css
---
* content
{:toc}

## 任务

- 使用 HTML 与 CSS 按照[示例图（点击查看）](http://7xrp04.com1.z0.glb.clouddn.com/task_1_3_1.png)实现三栏式布局。
- 左右两栏宽度固定，中间一栏根据父元素宽度填充满，最外面的框应理解为浏览器。背景色为 #eee 区域的高度取决于三个子元素中最高的高度。

## 左右固定中间自适应布局

html代码：

```html
<html>
<head>
    <meta charset="utf-8">
    <title>三栏布局</title>
</head>
<body>
    <div class="container">
        <div class="left">
            <img id="grouplogo" src="https://r11.fodey.com/2410/d056a0d89d2946dcafcf0751f7225e0e.1.gif" border: 0 width="80" height="80" >
            <div id="groupname">webGroup</div>
        </div>
        <div class="right">
            <img id="member1" class="memberlogo" src="img/code.png" title="张权">
            <img id="member2" class="memberlogo" src="img/touxiang.png" title="薛彬">
            <img id="member3" class="memberlogo" src="img/logo.jpg" title="农振立">
            <img id="member4" class="memberlogo" src="img/yangchenhao.png" title="杨晨昊">
            <img id="member5" class="memberlogo" src="img/wechat.jpg" title="王志文">
        </div>
        <div class="center">
            <h3 style="color:red;">webGroup</h3>
            <p>
                webGroup团队是百度前端学院2016级学院的一个小团队，由来自各地的前端兴趣小伙伴组成~成员共有五名，都想在此次学院中有所收获！
            </p>
            <strong><a href="http://axuebin.com/webGroup" target="_blank">团队主页(可以点一下哦~)</a></strong>
            <p><strong>张权:</strong>来自中国地质大学（武汉）计算机学院。作为程序猿，具备程序猿应有的气质和帅气！</p>
            <p><strong>薛彬:</strong>来自中国计量学院信息工程学院。喜欢看书和实践，热衷于解决具有挑战性的问题。<a href="http://axuebin.com" target="_blank">个人博客：http://axuebin.com</a></p>
            <p><strong>农振立:</strong>Believe that practice makes perfect.代码是敲出来的：坚信熟能生巧!<a href="mailto:nong99@outlook.com">   有事没事给我发邮件吧~</a></p>
            <p><strong>杨晨昊:</strong>一个在自学编程之路上努力探索的大四营销狗.Stay hungry, Stay foolish! <a href="http://chenhao-yang.github.io/" target="_blank">个人博客：http://chenhao-yang.github.io/</a></p>
            <p><strong>王治文:</strong>似乎是一名技术渣，从前幻想过做很多很多事情，但是都没有坚持下来，现在遇见了前端，真心喜欢并且希望能够坚持下去。</p>
        </div>
    </div>
</body>
</html>
```
附上css：

```css
    div{box-sizing: border-box;}
    .container,.left,.right,.center{padding:20px;border:1px solid #999;}
    .container {background-color: #eee;height: 580px;}
    .left {width: 200px;float: left;background-color: #fff;}
    .right {width: 120px;float: right;background-color: #fff;}
    .center {height: 400px;margin-left:220px;margin-right:140px;background-color: #fff;overflow:scroll}
    #grouplogo {width: 80px;height: 80px;float: left;}
    #groupname {font-weight: bold;color:darkblue;float: left;text-indent: 10px;}
    .memberlogo {width: 80px;height: 80px;border:1px solid #999;}
    #member1,#member2,#member3,#member4{margin-bottom:15px;}
    .center p{text-indent: 1cm; }
    .center a{text-decoration: none;}
```
## 参考资料

- [MDN：position](https://developer.mozilla.org/zh-CN/docs/Web/CSS/position)：了解 CSS position 属性的基本知识
- [MDN：float](https://developer.mozilla.org/en-US/docs/Web/CSS/float)：了解 CSS float 属性的基本知识
- [Learn CSS Positioning in Ten Steps](http://www.barelyfitz.com/screencast/html-training/css/positioning/)：通过具体的例子熟悉 position 属性
- [清除浮动（clearfix hack）](http://zh.learnlayout.com/clearfix.html)：清除浮动是什么，如何简单地清除浮动
- [StackOverflow](http://stackoverflow.com/questions/211383/which-method-of-clearfix-is-best)：Which method of ‘clearfix’ is best?：清除浮动黑科技完整解读

