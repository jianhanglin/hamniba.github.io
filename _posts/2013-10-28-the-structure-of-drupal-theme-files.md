---
layout: post
title: "Drupal Theme的文件结构"
description: "The structure of durpal theme files"
category: Drupal
tags: Drupal7 Theme
---

<br/>
###theme.info  
此文件是整个Theme的基本信息，包括name,description,package,version,core,需要用到的css，javascript文件和注册Theme页面的region信息。  
默认主题Bartik部分代码示例如下：  
	name = Bartik
	description = A flexible, recolorable theme with many regions.
	package = Core
	version = VERSION
	core = 7.x
	
	stylesheets[all][] = css/layout.css
	stylesheets[all][] = css/style.css
	stylesheets[all][] = css/colors.css
	stylesheets[print][] = css/print.css
	
	regions[header] = Header
	regions[help] = Help
	regions[page_top] = Page top
	regions[page_bottom] = Page bottom
	regions[highlighted] = Highlighted

###Template files(.tpl.php)  
> "These templates are used for the (x)HTML markup and PHP variables. In some situations they may output other types of data --xml, rss."  

Template files是指用户自定义theme下面的一些 *.tpl.php文件，比如 html.tpl.php; node.tpl.php; page.tpl.php; region.tpl.php等  
这些文件都是用户自定义的，若用户没有自定义这些文件，drupal将会使用默认的template files。  
Drupal默认template files，比如 modules/system里的html.tpl.php; page.tpl.php; modules/node里的node.tpl.php;modules/block里的block.tpl.php等。

###html.tpl.php  
这文件里面是一些基本的HTML结构，包含一些W3C规范和head信息，body就是一些变量信息。整个文件相当于只建好了一个Drupal站点的框架，站点的内容都由此文件里的变量完成。  
变量在template.php文件里通过两个function进行处理。  
	{% highlight php %}  
	function YOURTHEME_process_*();  
	function YOURTHEME_preprocess_*();  
	{% endhighlight %}  

###page.tpl.php  
此文件重点是处理一个HTML页面结构中的body部分，主要包含一些div tags and php code，php代码片段用于进行一些逻辑处理。  
html.tpl.php文件body中的语句  
	{% highlight php %}  
	<?php print $page; ?>  
	{% endhighlight %}  
其中变量$page指的就是这个page.tpl.php文件中的内容。  

###region.tpl.php  
此文件重点是处理Drupal站点上region的显示方式。  
变量`$classes`用于css文件，region命名方式用下划线: region_name; 该region对应的classes命名方式用破折号: class="region-page-top"。  

###node.tpl.php  
主要用于定义Drupal站点上node的显示方式，node里显示指定的`$content`。Drupal默认node.tpl.php位于modules/node。  
对于特殊的两个node，  
	{% highlight php %}  
	$content['comments']  
	$content['links']  
	{% endhighlight %}  
可以使用  
	{% highlight php %}  
	function hide();  
	print render();  
	{% endhighlight %}  
进行隐藏或显示。  

###field.tpl.php  
与其他template files不同的是，即使没有自定义的field.tpl.php，Drupal也不会自动加载默认field.tpl.php，若要使用，得从modules/fields/templates拷贝至你的自定义Theme中:YOURTHEME/templates。

###template.php  
> "For all the conditional logic and data processing of the output, there is the template.php file."  


作为初学者尤其需要注意的是，当你在自定义Theme里面添加或删除template files后，务必记得用你的admin账号登入你的Drupal站点，进入`admin/config/development/performance`清空你的站点缓存，否则你在自定义Theme下所做的修改将不会正确显示。  
> "Note: The [theme registry](https://drupal.org/node/173880#theme-registry) 
caches information about the available theming data. You must reset it when adding or removing template files or theme functions from your theme."  


<br/>
<br/>
<br/>
###参考资料：
---
* [Theming Guide](https://drupal.org/documentation/theme) `<- Drupal Documentation`  
* [Drupal 7 Theme Structure](http://ivansotof.com/2011/07/drupal-7-theme-structure/)  
