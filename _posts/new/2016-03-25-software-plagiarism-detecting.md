---
layout: post
title: 代码重复率检测
category: 技术
tags: research,moss,jplag
description: 代码抄袭检测
---
## 1.MOSS
[MOSS](http://theory.stanford.edu/~aiken/moss/ "moss")是斯坦福大学搞出的用于衡量程序相似性的自动系统，主要用于代码抄袭检测。

Supported Languages:

- C, C++, Java, C#, Python, Visual Basic, Javascript, FORTRAN, ML, Haskell, Lisp, Scheme, Pascal, Modula2, Ada, Perl, TCL, Matlab, VHDL, Verilog, Spice, MIPS assembly, a8086 assembly, a8086 assembly, MIPS assembly, HCL2.


Requirements:

- MOSS Account - [register](http://theory.stanford.edu/~aiken/moss/ "REGISTER")

ruby有个moss-ruby的gem
	
	gem install moss-ruby

**Uage**

- 安装gem
- 创建 MossRuby 项目
- 配置 MOSS 参数
- 远程调用MOSS服务，解析返回结果

代码如下：
{% highlight ruby %}
	require 'moss_ruby'

	# Create the MossRuby object
	moss = MossRuby.new(000000000) #replace 000000000 with your user id
	
	# Set options  -- the options will already have these default values
	moss.options[:max_matches] = 10
	moss.options[:directory_submission] =  false
	moss.options[:show_num_matches] = 250
	moss.options[:experimental_server] =    false
	moss.options[:comment] = ""
	moss.options[:language] = "c"
	
	# Create a file hash, with the files to be processed
	to_check = MossRuby.empty_file_hash
	MossRuby.add_file(to_check, "The/Files/Path/MyFile.c")
	MossRuby.add_file(to_check, "Other/Files/Path/*.c")
	MossRuby.add_file(to_check, "Many/Files/Paths/**/*.h")
	
	# Get server to process files
	url = moss.check to_check
	
	# Get results
	results = moss.extract_results url
	
	# Use results
	puts "Got results from #{url}"
	results.each { |match|
	    puts "----"
	    match.each { |file|
	        puts "#{file[:filename]} #{file[:pct]} #{file[:html]}"
	    }
	}
{% endhighlight %}

## 2.JPLAG
[JPlag](https://github.com/jplag/ "jplag")也可以检测代码抄袭，而且还是开源的，使用java编写的，需要有java环境，通过下面的形式调用：

    java -jar jplag-yourVersion.jar -l java17 -r /tmp/jplag_results_exerise1/ -s /path/to/exercise1

- -l java17 tells JPlag to use the frontend for Java 1.7
- -s tells JPlag to reccurse into subdirectories; as we assume Java projects, we'll very likely encounter subdirectories such as student1/src/
- -r /tmp/jplag_results_exercise1 tells JPlag to store the results in the directory /tmp/jplag_results_exercise1

输出结果如下：

{% highlight bash %}
	Language accepted: C/C++ Scanner [basic markup]
	Command line: -l c/c++ /home/other/Desktop/postingshighlight 
	initialize ok
	2 submissions

	2 submissions parsed successfully!
	0 parser errors!


	Comparing future_net (copy).cpp-future_net.cpp: 100.0

	Writing results to: result
{% endhighlight %}


用Ruby调用并提取结果：
{% highlight ruby %}
    `java -jar jplag.jar -l #{language} #{dir}`.each_line do |line|
    	puts line.split(" ",2)[1] if line.match("Comparing")
	end
{% endhighlight %}
	


