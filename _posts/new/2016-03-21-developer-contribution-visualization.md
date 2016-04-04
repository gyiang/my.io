---
layout: post
title: 开发者贡献度量可视化
category: 技术
tags: research,visualization,R
description: 可视化开发者贡献的各个指标，研究演化趋势
---
使用数据集来自[elastic/elasticsearch](https://github.com/elastic/ 'elasticsearch')

通过github和本地clone仓库，使用脚本计算各个待度量指标，其中kimchy的数据集是这个样子的：

![es-k-contribution-metric-data](http://7xr422.com1.z0.glb.clouddn.com/es-k-contribution-metric-data.png)

使用R中的ggplot2来一种创新可是化方法：

{% highlight r %}
my_set<-read.csv('users_radar_k_line.csv')

library(reshape2)
library(ggplot2)
library(scales)

maxmin <- data.frame(
  ADD   = c(max(my_set$add), min(my_set$add)),
  DEL = c(max(my_set$del), min(my_set$del)),
  CMT  = c(max(my_set$cmt), min(my_set$cmt)),
  FIX = c(max(my_set$fixs), min(my_set$fixs)),
  CLOSES = c(max(my_set$closes), min(my_set$closes)),
  ISSUES = c(max(my_set$issues), min(my_set$issues)),
  COMMENTS=c(max(my_set$comments), min(my_set$comments))
)
dat <- data.frame(
  ADD   = my_set$add,
  DEL = my_set$del,
  CMT  = my_set$cmt,
  FIX = my_set$fixs,
  CLOSES = my_set$closes,
  ISSUES=my_set$issues,
  COMMENTS=my_set$comments
 
)

# 标准化数据
normalised_dat <- as.data.frame(mapply(
  function(x, mm)
  {
    (x - mm[2]) / (mm[1] - mm[2])
  },
  dat,
  maxmin
))

normalised_dat$tag<-my_set$tag
long_dat <- melt(normalised_dat, id.vars = "tag")

ggplot(long_dat, aes(x = variable, y = value, colour = tag, group = tag)) +
  geom_line()+
  coord_polar(theta = "x", direction = 1) +
  scale_y_continuous(labels = percent)+
  labs(title = "kimchy,cmt=4779")+theme(axis.title.x=element_blank(),axis.title.y=element_blank())
#+theme(legend.position='none');
{% endhighlight %}

效果图如下：

![es-k-radar-chart-a-star-plot](http://7xr422.com1.z0.glb.clouddn.com/es-k-radar-chart-a-star-plot.png)


![visualization-meanings](http://7xr422.com1.z0.glb.clouddn.com/es-kradar-chart-a-star-plot-detail.png)

继续按照时间序列，画各个度量指标的演化趋势

{% highlight r %}
t_scale<-data.frame(scale(my_set[,2:8], center=F,scale=T))
t_scale$date<-my_set$date
data_long <- melt(t_scale, id="date")
ggplot(data_long,aes(x=as.Date(date),y=value,colour=variable))+geom_point()+geom_line()+
  theme(axis.title.x=element_blank(),axis.title.y=element_blank())+labs(title = "kimchy")
{% endhighlight %}

这个图相对就比较直观了：

![](http://7xr422.com1.z0.glb.clouddn.com/es-k-metric-line.png)

上面图的具体含义：

![visualization-meanings](http://7xr422.com1.z0.glb.clouddn.com/es-k-metric-line-detail.png)


