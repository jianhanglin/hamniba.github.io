---
layout: post
title: "Node.js入门"
description: 
category: Node.js
tags: microblog
---
<br/>

![Microblog](./media/images/frontpage.png)


前后花了大概一天半的时间从头到尾看完了《Node.js开发指南》([BYVoid](https://www.byvoid.com/)编著)。  
看完这本书，就算是Node.js开发入门了，里面有个小型的Web项目练习，作者一步步讲解得很详细，从Node.js开发的基础，到Web开发领域的通用知识点，都作了详细介绍，
照着这本书的流程包括项目实践走一遍下来肯定会收获不小。

不过，在练习书中项目的过程中，会遇到很多的问题。因为本书著于2012年，由于时间原因项目中的Express版本发生了变化，
从2.X发展到3.X其中有很多需要改动的地方，不然会不停的报错，比如项目中有些方法的调用会不同，
或者某些方法在新版本中已经不存在了，版本变化导致的具体差异和解决方法我会在下方给出个链接，方便查阅。
在项目中遇到的问题可以去[Node.js中文社区](http://cnodejs.org/)查阅或提问，一般都会有解决方案的，因为社区里大部分人都做过这个项目，也都曾被版本问题所困扰。

这个练习项目的整个框架我已经照着教程搭起来了，并能在本地顺利跑起来。但其中还有一些知识点，比如MongoDB的用法，Express的用法，ejs模板的用法，常用第三方module的用法等等，
这些都还得花时间参考官方文档学习。

我现在已经把这个项目放到了Github上，计划在我对Node.js越来越熟练的时候，逐渐给它添加一些新功能，使这个微博平台更完善，在学习Node.js的过程中就把它当做小白鼠吧。

<br/>
<br/>
<br/>
参考资料：
----------
* [Migrating from 2.x to 3.x](https://github.com/visionmedia/express/wiki/Migrating-from-2.x-to-3.x)
* [使用Express3.0实现<Node.js开发指南>中的微博系统](http://www.cnblogs.com/meteoric_cry/archive/2012/07/23/2604890.html)
* [项目Github地址](https://github.com/Hamniba/Microblog)  
