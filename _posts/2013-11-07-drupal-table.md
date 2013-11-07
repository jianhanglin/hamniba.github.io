---
layout: post
title: "用Drupal的方式写Table"
description: "The function themem_table() of Drupal."
category: Drupal
tags: Drupal7 Theme
---
<br>
要在Drupal里面写table可以有两种实现方式，一种是全部使用html标签，另一种是用drupal提供的`theme_table()`方法实现。  

在Drupal核心的`theme.inc`里面`theme_table()`方法是如下定义的：  

	{% highlight php %}
	<?php
	function theme_table($variables) {
		$header = $variables['header'];
		$rows = $variables['rows'];
		$attributes = $variables['attributes'];
		$caption = $variables['caption'];
		$colgroups = $variables['colgroups'];
		$sticky = $variables['sticky'];
		$empty = $variables['empty'];
		}
	?>
	{% endhighlight %}  
你可以对这个`theme_HOOK()`方法用`theme('HOOK',$variables)`函数进行覆写，比如这里的`theme('table',$variables)`。  

注意：  
> "在你的模块中任何需要输出HTML或者XML的部分都应该使用以"theme_"开头的主题函数，这样设计者就可以对它们进行覆写了。"  

`$variables`变量是一个数组,`$variables = array();`比如定义一个`$table`变量：

	{% highlight php %}
	<?php
	$table = array(
        'header' => $header,
        'rows' => $rows,
		'attributes' =>'',
        'caption' => '', 
		'colgroups' => '',
        'sticky' => FALSE, 
        'empty' => 'Do not have any rows here...',
            )
    );  
	?>
	{% endhighlight %}
###$header
	$header = array();
* `'data'`: 指定header的title;  
* `'field'`: 是与table列名(title)相对应的数据库里面的field，用于数据库操作。  
* `'sort'`: 对table中的某一列进行排序`('asc' or 'desc')`升序或降序排列。  
#####e.g.  
		{% highlight php %}
	<?php
		$header = array(
        	array('data' => t('Name')),
        	array('data' => t('Age'), 'field' => 'age'),
        	array('data' => t('Gender')),
        	array('data' => t('Birth'), 'sort' => 'asc'),
        	array('data' => t('Description')),
    	);
	?>
		{% endhighlight %}

###$rows	
	$rows = array();
`$rows`定义的是table中每一行的结构，且应该与`$header`的title对应，`$rows`需要放在for循环中使用。  

	foreach ($order_nodes as $nodeitem)

* `'data'`: `'data' => array()`也是一个数组，里面存放的是table中每一行各单元格的值。  
* `'no_striping'`: 是一个boolean值，默认是FALSE。指定奇数行或者偶数行是否需要不同的显示样式，比如将一个表格奇数行表现为白色偶数行表现为黄色。  
* 对于复杂的嵌套table,还可以分别对row的特定单元格指定你希望定义样式，比如row cell里嵌套`$header`。所以，每个单元格还可以独立设置它的`'data'`和`'header'`。  
#####e.g.
		{% highlight php %}
	<?php
		$rows = array(
            'data' => array(
                $name,
                $age,
                $gender,
                $date_of_birth,
                $description,
            )
		);
	?>
		{% endhighlight %}

###'attribute'
这是HTML中的attribute属性值，应用于整个table。  

	'attribute' => array('class' => array('myclass')),
也可以在每个`$header`或`$rows`里面单独使用`'attribute'`属性来定义样式。

###'caption'
HTML里面的`<caption>`标签，用于指定整个table的显示标题。`->`[caption tag](http://www.w3schools.com/tags/tag_caption.asp)

###'colgroups'
HTML里面的`<colgroup>`标签，用于将列(column)分组，统一定义样式。`->`[colgroup tag](http://www.w3schools.com/tags/tag_colgroup.asp)

###'sticky'
布尔值，用于是否将table中的标题(header)始终置于页面顶端显示。比如一个表格，当你鼠标向下滑动浏览的时候，表格header部分可以始终悬浮于页面顶端。  
> "Use a "sticky" table header to indicate whether the table headers should be sticky."

###'empty'
table中行数(row)为零时显示的提示信息。  
###Display the table
最后在`$table`的结构定义好之后，就可以用`theme('HOOK',$variables)`这个方法调用显示：  

	{% highlight php %}
	<?php
	$html = theme('table', array(
        'header' => $header,
        'rows' => $rows,
        'caption' => '',
        'sticky' => FALSE,
        'empty' => 'Do not have any rows here...',
        )
    );
	?>
	{% endhighlight %}

<br/>
<br/>
<br/>
参考资料：
----------
* [theme_table](https://api.drupal.org/api/drupal/includes!theme.inc/function/theme_table/7)` <-Drupal Documentation`  
* [function theme](https://api.drupal.org/api/drupal/includes!theme.inc/function/theme/7)` <-Drupal Documentation`  
* [覆写drupal主题函数](http://www.thinkindrupal.com/node/1063)


