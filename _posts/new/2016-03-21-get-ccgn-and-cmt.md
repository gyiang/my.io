---
layout: post
title: git统计贡献提交次数和代码变更行数
category: 技术
tags: research,git
description: 统计git代码库中每个贡献者提交次数和代码变更行数
---
## 统计
使用git log命令去获取所有提交信息，然后结合ruby脚本进行处理

{% highlight ruby %}
git_tree="--git-dir=/root/Desktop/elasticsearch/.git"
#total commits,contributors
total_commits=`git #{git_tree} log --pretty=oneline | wc -l`.to_i
h={}
#each contributor
`git #{git_tree}  log --pretty='%an,%ae' | sort | uniq -c | sort -k1 -n -r `.each_line do |line|
  commits_num, user=line.chomp.split(" ", 2)
  uname, email=user.split(",")

  add, del, changes=`git #{git_tree}  log --author="#{uname}" --pretty=tformat: --numstat |
 gawk '{ add += $1;subs += $2;loc += $1 + $2} END {printf("%s,%s,%s",add,subs,loc)}' -`.split(",")

  percentage="%.2f" % (Float(commits_num)/total_commits*100) +"%"

  p [percentage,commits_num, uname, email, add, del, changes.to_i.abs]	
end
{% endhighlight %}

## git log 输出格式化
	git log --pretty=format:"%h" 
git用各种placeholder来决定各种显示内容： 

- %H: commit hash
- %h: 缩短的commit hash
- %T: tree hash
- %t: 缩短的 tree hash
- %P: parent hashes
- %p: 缩短的 parent hashes
- %an: 作者名字
- %aN: mailmap的作者名字 (.mailmap对应，详情参照git-shortlog(1)或者git-blame(1))
- %ae: 作者邮箱
- %aE: 作者邮箱 (.mailmap对应，详情参照git-shortlog(1)或者git-blame(1))
- %ad: 日期 (--date= 制定的格式)
- %aD: 日期, RFC2822格式
- %ar: 日期, 相对格式(1 day ago)
- %at: 日期, UNIX timestamp
- %ai: 日期, ISO 8601 格式
- %cn: 提交者名字
- %cN: 提交者名字 (.mailmap对应，详情参照git-shortlog(1)或者git-blame(1))
- %ce: 提交者 email
- %cE: 提交者 email (.mailmap对应，详情参照git-shortlog(1)或者git-blame(1))
- %cd: 提交日期 (--date= 制定的格式)
- %cD: 提交日期, RFC2822格式
- %cr: 提交日期, 相对格式(1 day ago)
- %ct: 提交日期, UNIX timestamp
- %ci: 提交日期, ISO 8601 格式
- %d: ref名称
- %e: encoding
- %s: commit信息标题
- %f: sanitized subject line, suitable for a filename
- %b: commit信息内容
- %N: commit notes
- %gD: reflog selector, e.g., refs/stash@{1}
- %gd: shortened reflog selector, e.g., stash@{1}
- %gs: reflog subject
- %Cred: 切换到红色
- %Cgreen: 切换到绿色
- %Cblue: 切换到蓝色
- %Creset: 重设颜色
- %C(...): 制定颜色, as described in color.branch.* config option
- %m: left, right or boundary mark
- %n: 换行
- %%: a raw %
- %x00: print a byte from a hex code
- %w([[,[,]]]): switch line wrapping, like the -w option of git-shortlog(1).