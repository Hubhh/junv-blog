---
layout: post
title: "Let Travis-CI help windows bloger run Octopress Build"
date: 2013-01-01 00:35
comments: true
categories: 
  - talk
tags:
  - travis_ci
  - github
  - octopress
---
这是我2013年的第一篇日志，本来不会来的这么快的，结果没想到来得比2002年的第一场雪还快。初衷是这样的，我打算在windows平台下使用Octopress写博客，但是我发现有各种各样的问题来阻扰我完成这个任务：RVM 不能安装、Bundle install 报错，在我bundle install 完成之后，我以为这下应该好了，结果在执行 **rake generate**生成内容的时候还是有问题。总之各种问题，最终我放弃了在windows下去执行这个命令，Travis-CI是这么好的一个免费并且开源的持续集成工具，为什么我们不用呢，于是就有了今天这篇博客。  

首先你得去[Octopress]()官方去看他的使用手册，Octopress他本身的Git仓库，和我们最终写出的博客的那个仓库不是同一个仓库。我们的博客仓库是用Octopress仓库中source目录执行 rake generate生成的。因此我们需要放到Travis-CI上进行编译的就是Octopress仓库，不过我们得给他加点配置东西：Travis-CI配置文件。

我们在Octopress根目录创建一个 `.travis.yml` 的文件，文件的内容如下：  
		rvm:  
 		 - 1.9.3  
		script:  
  		- RAILS_ENV=test bundle exec rake generate --trace  
这个文件就告诉Travis-CI，在编译我们的项目的时候去执行 `rake generate` 这样就达到了我们想要通过编译来知道我们写的博客是否格式正确，是否能编译成功的目的。 
