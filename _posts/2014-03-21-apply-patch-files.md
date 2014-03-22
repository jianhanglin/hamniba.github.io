---
layout: post
title: "如何给第三方Module文件打上补丁"
description: 
category: Drupal
tags: drupal-7
---
<br/>
#How to Apply patch files


使用Drupal社区贡献的第三方Module出现Bug的时候，针对遇到的问题或Bug在该Module's issues页面里找到对应Bug的补丁文件，通常是 *.patch，将该文件下载下来放置在你需要修复的Module的根目录下。  
然后在终端里面用patch命令执行补丁，patch命令是内置在Linux/Unix系统里面的。  

`patch < patchname.patch`  
此命令之后终端会提示你指定需要打上补丁的文件路径及文件名。`File to patch:`

如果是要修复Drupal核心代码的Bug，需要将补丁文件放在Drupal的根目录下执行(patch from the drupal root directory )，命令最好加上参数：  
`patch -p0 < patchname.patch`  
加上这个参数，patch命令就不会再询问你“需要给哪个文件打补丁”了。  

如果补丁文件里面包含'a & b directories'这样的字段，例如`diff --git a/path/to/file b/path/to/file`，可以使用以下命令：  
(you can use the `-p1` parameter to get rid of the a/b directories.)    
`patch -p1 < patchname.patch`

如果测试发现打上补丁之后并没有修复已知的Bug，可以使用以下命令将文件还原(Revert)到打补丁之前的状态：  
`patch -p0 -R < patchname.patch`  
需要注意在还原之前，原文件中被补丁修改过的代码不要有任何改动，例如人为加上任何多余的空行或者注释都是不可以的。

当然你也可以根据找到的补丁文件，先看懂补丁里面代码表示的意思，知道它需要改动的是哪个文件以及哪段代码，然后参照补丁里面的方法对代码手动的增删改。此方法不推荐。

打补丁需要注意的是：
  
1. 尽量在Drupal官方社区里面找补丁文件，通常Module都会有一个issues页面，上面列出了已知Bug以及该Bug的解决方案和补丁，尽量使用issued status为"Reviewed & tested by the community"的补丁。
2. 对于没有经过社区或Module维护者测试过的补丁，不要直接用在你已上线的项目上，最好是在本地测试好补丁已正确修复Bug而且没有引发其他的错误，方可上传至项目中。



<br/>
<br/>
<br/>
####更多注意事项和参考资料：  
[Applying patches on Mac OS X](https://drupal.org/node/60818)  
[Apply patches on Windows](https://drupal.org/node/60179)  
[HowTo: How to apply a patch to a contributed module - Beginner's version ](https://drupal.org/node/620014)  
[Applying a patch manually](https://drupal.org/node/534548)
