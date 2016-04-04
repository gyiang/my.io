---
layout: post
title: Jekyll的中的代码高亮
category: 工具
tags: Jekyll
description: jekyll代码高亮
---

### 代码高亮方式选择

#### 1.小片段 

直接使用“ \` ”符号包含起来，或者使用一个tab直接利用markdown来做高亮

#### 2.Pygments渲染
  
Jekyll通过[Pygments](http://pygments.org/)可以直接处理代码高亮

在Github Pages的[文档](https://github.com/mojombo/jekyll/wiki/Liquid-Extensions)里，也提到了这个方式，但是有个问题，这种方式打破了markdown的格式

_config.xml配置：

{% highlight xml %}
kramdown:
  input: GFM
  extensions:
    - autolink
    - footnotes
    - smart
  use_coderay: true
  syntax_highlighter: rouge
  coderay:
    coderay_line_numbers:  nil
{% endhighlight %}

在文章中，使用

\{\% highlight xxx \%\}

code

\{\% endhighlight \%\}

引用代码



#### 3.gist嵌入方式

这个[方式](https://gist.github.com/imathis/1027674)使用了一个插件，而且gist也得管理，增大了开销……

#### 4.js和css处理

这个方式使用了[google-code-prettify](https://code.google.com/p/google-code-prettify/)来渲染代码高亮，本身库并不是很大，使用方便

### Prettify使用

#### 1.下载代码

直接到[google-code-prettify](https://code.google.com/p/google-code-prettify/)官网下载代码，然后将它们放到项目下

#### 2.包含css和js

官网提到了可以直接包含run_prettify.js的方式，这个会导入远程库，选择了自己导入，如下

{% highlight js %}
<link rel="stylesheet" href="/public/js/prettify/prettify.css">
<script src="/public/js/prettify/prettify.js"></script>
<script type="text/javascript">
  $(function(){
    $("pre").addClass("prettyprint linenums");
    prettyPrint();
  });
</script>
{% endhighlight %}

这里导入了css和js后，就可以直接用markdown的tab的方式来导入代码段了

#### 3.更换主题
默认主题不是很好看，只要更换prettify.css即可更换样式，可以到[这里](http://google-code-prettify.googlecode.com/svn/trunk/styles/index.html)下载自己喜欢的主题css即可

