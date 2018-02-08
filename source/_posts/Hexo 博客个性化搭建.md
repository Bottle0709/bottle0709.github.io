---
title: Hexo 博客个性化搭建
date: 2018-01-8 11:47:40
update: 2018-01-15 18:35:34
top: 80
tags:
- css
- html
categories: Hexo
password:
cover_picture: http://p3nn031ge.bkt.clouddn.com/blog/180208/0L7IC6C2A8.png?imageslim
---
![mark](http://p3nn031ge.bkt.clouddn.com/blog/180208/0L7IC6C2A8.png?imageslim)
## 前言
&emsp;博客基本框架搭建起来了，但不是很满意。于是下一步要做的就是添加想要实现的功能。在此过程中通过查网上资料且不断的折腾代码，完成如今的博客，还是有些缺陷，日后再修改，在此记录下我是如何实现这些功能的，以免过后遗忘。
## 一、框架功能添加

### &emsp;1.增加新的导航菜单
&emsp;在 Hexo里，默认的导航菜单只有`Home`和`Archives`两项，那么如何增加新的导航菜单进去？

&emsp;首先，打开主题的配置文件`_config.yml`
&emsp;之后我们会看到`menu:`，这个部分是设置菜单的，在下面加一想设置`About: /about`，前面部分是名称，后面部分是访问路径。
```java
   menu:
     Home: /
     Archives:/archives
     About: /about
```
&emsp;设置好后，通过运行命令，建立 about，会在 source 目录里生成一个对应的about目录，该目录下的 index.md，就是访问 About 时的页面。
```
   hexo n page 'about'
```

### &emsp;2.修改头像并旋转
&emsp;**实现方法：**
打开`\themes\miho\source\css\_partial\header.styl`，在里面添加如下代码：
```css
#logo
  @extend $logo-common
  margin: 20px auto 
  img
    border-radius: 50%
    transition: all 1.6s cubic-bezier(.17,.67,.62,1.22)
    -webkit-transition: all 1.6s cubic-bezier(.17,.67,.62,1.22)
    -moz-transition: all 1.6s cubic-bezier(.17,.67,.62,1.22)
    -o-transition: all 1.6s cubic-bezier(.17,.67,.62,1.22)
    -ms-transition: all 1.6s cubic-bezier(.17,.67,.62,1.22)
    &:hover
      transform: rotate(360deg);
      -ms-transform: rotate(360deg); /* IE 9 */
      -webkit-transform: rotate(360deg); /* Safari and Chrome */
```
&emsp;**实现效果：**
![mark](http://p3nn031ge.bkt.clouddn.com/blog/180205/l14H2I6cFb.jpg?imageslim)

### &emsp;3.设置网站的图标Favicon
&emsp;**实现方法：**
&emsp;在网站下载或是制作，并将图标名称改为`favicon.ico`,然后把图标放在`/themes/miho/source/images`里，并修改主题配置文件：
```css
# Favicon of your site | 网站icon
favicon: /favicon.icon
```
&emsp;**实现效果：**
![mark](http://p3nn031ge.bkt.clouddn.com/blog/180205/5hAGcH7Abm.png?imageslim)

### &emsp;4.在网站底部加上访问量
&emsp;**实现方法：**
&emsp;打开`\themes\miho\layout\_partial\plugins\sites\visit.ejs`文件，添加如下代码：
```css
<span id="busuanzi_container_site_pv" style='display:none'>
        <%- theme.access_counter.site_pv %><span id="busuanzi_value_site_pv"></span>
    </span>
```
&emsp;**实现效果：**
![mark](http://p3nn031ge.bkt.clouddn.com/blog/180205/bIDLDb835C.png?imageslim)

### &emsp;5.增加图床

&emsp;**实现方法：**
&emsp;写博客避免不了常常使用图片,可是Github Pages是有容量限制的,不可能全部都作为静态文件进行上传。在此使用一个大多博主推荐的“七牛云图床”。七牛云不是免费的，但每个用户有10GB免费存储，每月10GB免费下载流量,需要验证身份证等个人信息。使用方法:
&emsp;1.打开链接并注册,单机 对象存储–>创建空间。
![mark](http://p3nn031ge.bkt.clouddn.com/blog/180205/8aL61FmeFA.png?imageslim)

&emsp;2.下载 MPic，下载后设置账号

![mark](http://p3nn031ge.bkt.clouddn.com/blog/180205/J17KHm0bBD.png?imageslim)

>   1).在“个人面板”->“密钥管理”中查看 AccessKey/SecretKey；
>   2).在储存空间的“空间概览”里，记住这里的“测试域名”；
>   3).在MPic上配置上刚才七牛储存的“空间名称”、“AccessKey”、“SecretKey”、“域名”后，保存。然后就可以上传到自己专属的七牛空间上了。

## 二、文章功能添加

### &emsp;1.主页文章添加阴影效果
&emsp;**实现方法：**
打开`\themes\miho\source\css\_partial\header.styl`,向里面加入：
```java
// 主页文章添加阴影效果
 .post {
   margin-top: 60px;
   margin-bottom: 60px;
   padding: 25px;
   -webkit-box-shadow: 0 0 5px rgba(202, 203, 203, .5);
   -moz-box-shadow: 0 0 5px rgba(202, 203, 204, .5);
  }
```
### &emsp;2.修改``代码块自定义样式

&emsp;**实现方法：**
```java
.article-entry code {
    color: #c7254e;
    line-height: 1;
    margin: 0 4px;
    font-size: 85%;
    font-family: "Source Code Pro", Consolas, Monaco, Menlo, Consolas, monospace;
    font-size: 1em;
    padding: 2px 4px;
    border: 1px solid #eee;
    border-radius: 2px;
    word-wrap: break-word;
    background-color: #f9f2f4;
}
```
&emsp;**实现效果：**
![mark](http://p3nn031ge.bkt.clouddn.com/blog/180205/ld4E4CGGgF.png?imageslim)

### &emsp;3.在每篇文章末尾统一添加"本文结束"标记
&emsp;**实现方法：**
&emsp;在路径 `\themes\miho\layout\_partial\post` 中新建 `passage-end-tag.ejs` 文件,并添加以下内容：
```java
 <div style="text-align:center;color: #B8B8B8;font-size:22px;">-------------本文结束 <i class="fa fa-paw"></i> 感谢您的阅读-------------</div>
```
&emsp;**实现效果：**
![mark](http://p3nn031ge.bkt.clouddn.com/blog/180205/2iFah71fc9.png?imageslim)

### &emsp;4.添加来必力评论
&emsp;**实现方法：**
```java
<% if (!index && post.comments){ %>
    <% if (theme.changyan_appid && theme.changyan_appkey){ %>
        <%- partial('plugins/comments/changyan', {
            key: post.slug,
            title: post.title,
            url: config.url+url_for(post.path)
        }) %>
    <% } else if (theme.youyan_id) { %>
        <%- partial('plugins/comments/youyan') %>
     <% } else if (theme.livere_uid) { %>
        <%- partial('plugins/comments/livere') %>
        <div id="lv-container" data-id="city" data-uid="<%= theme.livere_uid %>"></div>
    <% }else if (theme.disqus || config.disqus_shortname) { %>
        <section id="comments">
            <div id="disqus_thread">
                <script type="text/javascript">
                    var disqus_shortname = '<%= theme.disqus || config.disqus_shortname %>';
                    (function() {
                        var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
                        dsq.src = '//' + disqus_shortname + '.disqus.com/embed.js';
                        (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
                    })();
                </script>
                <noscript>Please enable JavaScript to view the <a href="//disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
            </div>
        </section>
    <% } %>
<% } %>
```
&emsp;**实现效果：**
![mark](http://p3nn031ge.bkt.clouddn.com/blog/180205/7J2EHc6eD4.png?imageslim)

### &emsp;5.博文置顶
&emsp;**实现方法：**
&emsp;修改 `hero-generator-index` 插件，把文件：`node_modules/hexo-generator-index/lib/generator.js` 内的代码替换为：
```java
'use strict';
var pagination = require('hexo-pagination');
module.exports = function(locals){
  var config = this.config;
  var posts = locals.posts;
    posts.data = posts.data.sort(function(a, b) {
        if(a.top && b.top) { // 两篇文章top都有定义
            if(a.top == b.top) return b.date - a.date; // 若top值一样则按照文章日期降序排
            else return b.top - a.top; // 否则按照top值降序排
        }
        else if(a.top && !b.top) { // 以下是只有一篇文章top有定义，那么将有top的排在前面（这里用异或操作居然不行233）
            return -1;
        }
        else if(!a.top && b.top) {
            return 1;
        }
        else return b.date - a.date; // 都没定义按照文章日期降序排
    });
  var paginationDir = config.pagination_dir || 'page';
  return pagination('', posts, {
    perPage: config.index_generator.per_page,
    layout: ['index', 'archive'],
    format: paginationDir + '/%d/',
    data: {
      __index: true
    }
  });
};
```
&emsp;在文章中添加 `top` 值，数值越大文章越靠前，如
```html
---
title: 解决Charles乱码问题
date: 2017-05-22 22:45:48
tags: 技巧
categories: 技巧
copyright: true
top: 100
---
```
## 三、页面功能添加

### &emsp;1.项目页面
&emsp;**实现方法：**
```java
<div class="container">
  <h2 class="ctitle"><b>个人作品集</b></h2>
       <div class="gbook">
            <div class="about">
               <div class="about_girl"><span><a href="/"><img src="<%= url_for(theme.pro) %>" alt="logo"></a></span>
               <p>凡是重要的事，都得花上很多的时间，而且是完整的大块时间。不论是讨论一种新产品还是重大的人事决策，几乎所有的事情都是如此。</p>
               </div>
            </div>
       </div>
   <div class="works-item">
       <ol class="repo-list">
        <% for(var i in theme.project){ %>
          <li class="repo">
                <div class="works-item">
                    <div class="title">
                        <h3> <%- theme.project[i].title %></h3>
                        <span class="title-date"> <%- theme.project[i].data %> </span>
                    </div>
                    <div class="works-item-img">
                        <img src="<%- theme.project[i].img_link %>">
                    </div>
                        <span class="use"> <%- theme.project[i].arrayVal %> </span>
                        <p class="subtitle"> <%- theme.project[i].subTitle %> </p>
                        <p class="text-muted"> <%- theme.project[i].direction %> </p>
                    <div class="footer clearfix">
                        <a class=" btn btn-default" href="<%- theme.project[i].link %>" target="_blank"> Open
                            it</a>
                    </div>
                </div>
                </li>
                <% } %>
   </ol>
         </div> 
</div>
```
&emsp;**实现效果：**
![mark](http://p3nn031ge.bkt.clouddn.com/blog/180205/D941FBj9c5.png?imageslim)

### &emsp;2.留言页面
&emsp;**实现方法：**
```java
<div class="container">
    <h2 class="ctitle">
    <b>留言板</b> 
    <span>你，生命中最重要的过客，之所以是过客，因为你未曾为我停留。</span>
    </h2>
    <div class="gbook">
      <div class="about">
        <div id="fountainG">
          <li></li>
          <li></li>
          <li></li>
          <li></li>
          <li></li>
          <li></li>
          <li></li>
          <li></li>
        </div>
        <div class="about_girl"><span><a href="/"><img src="<%= url_for(theme.logo) %>" alt="logo"></a></span>
          <p>当您驻足停留过，从此便注定我们的缘分。站在时间的尽头，我们已是朋友，前端的路上我再也不用一个人独自行走。</p>
        </div>
        <div class="gbko">
        <% if (theme.changyan_appid && theme.changyan_appkey){ %>
        <%- partial('/plugins/comments/changyan', {
            key: post.slug,
            title: post.title,
            url: config.url+url_for(post.path)
        }) %>
    <% } else if (theme.youyan_id) { %>
        <%- partial('plugins/comments/youyan') %>
     <% } else if (theme.livere_uid) { %>
        <%- partial('plugins/comments/livere') %>
        <div id="lv-container" data-id="city" data-uid="<%= theme.livere_uid %>"></div>
    <% }else if (theme.disqus || config.disqus_shortname) { %>
        <section id="comments">
            <div id="disqus_thread">
                <script type="text/javascript">
                    var disqus_shortname = '<%= theme.disqus || config.disqus_shortname %>';
                    (function() {
                        var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
                        dsq.src = '//' + disqus_shortname + '.disqus.com/embed.js';
                        (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
                    })();
                </script>
                <noscript>Please enable JavaScript to view the <a href="//disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
            </div>
        </section>
    <% } %>
        </div>
    </div>
  </div>
</div>
```
&emsp;**实现效果：**
![mark](http://p3nn031ge.bkt.clouddn.com/blog/180205/hDBLCIlaEI.png?imageslim)

### &emsp;3.关于页面
&emsp;**实现方法：**
```java
<div id="cont">
  <marquee style="height: 140px;" scrollamount="2" direction="down" behavior="slide">
    <div class="banner">
      <p>我们不停的翻弄着回忆，却再也找不回那时的自己</p>
      <p>人生，是一场盛大的遇见。若你懂得，就请珍惜。</p>
      <p>无论下多久的雨，最后都会有彩虹；无论你多么悲伤，要相信幸福在前方等候.</p>
    </div>
       </marquee>
    <div class="about left">
     <h2>Just about me</h2>
       <ul> 
           <p>关于我，一个未来的小小码农，茫茫宇宙中的一粒小石子。</p>
           <p>凭借着兴趣已经走过了三个年头，现在已经是大四的老油条，但总的来说还是一个刚步入社会的新人。</p>
           <p>很喜欢交朋友， 下面是我的微信二维码， 欢迎看到博客的朋友加我好友， 多给我提提意见， 多讨论讨论技术，三人行， 则必有我师 !</p>
           <p align="center">微信请备注：博客</p>
           <p><img src="/images/wechat_code.jpg" alt=""></a></p>
           <p></p>
       </ul>
     <h2>About my blog</h2>
         <p>域  名：暂无</p>
         <p>服务器：托管于 Github，欢迎 Fork </p>
         <p>折腾开始于2018年1月2日，基本在2018年1月16完工。</p>
         <p>一直想有个自己的博客，写写个人学习、工作感悟什么的，当然也会有一些IT类的文章,这次就借助hexo+Github page 搭建了这个博客，第一次搭建还是有些粗糙，以后会逐渐改进。。。</p>
         
     <h2>Contact Me</h2>
     <p>新浪微博：<a href="http://weibo.com/tongliping0709" class="blog_link">点击进入我的新浪微博（可以加个关注哈）</a></p>
     <p>知乎：<a href="https://www.zhihu.com/people/tian-hao-69-26" class="blog_link">点击进入我的知乎</a></p>
     <p>Github:  <a href="https://github.com/tongliping0709" class="blog_link">点击进入我的github ( 欢迎fork me )</a></p>
    </div>
</div>
```
&emsp;**实现效果：**
![mark](http://p3nn031ge.bkt.clouddn.com/blog/180205/9LcD2HchAJ.png?imageslim)