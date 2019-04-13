---
layout: post
title: GitHub pages 搭建博客
date: 2019-02-24 15:32:24.000000000 +09:00
---

# 本地环境初始化
## 安装 ruby
- (下载地址](https://www.ruby-lang.org/en/downloads/)
- 安装后使用 `ruby -v` 进行验证

## 安装 jekyll
- 使用命令 `gem install jekyll` 进行安装
- 大陆用户可使用 taobao 的 ruby 源，具体操作如下
```bash
gem sources --remove https://rubygems.org/
gem sources -a https://ruby.taobao.org/
gem sources -l
```

## 安装 bundler 包管理器
- 使用命令 `gem install bundler` 进行安装
- 在你的 GitHub pages 根目录创建文件 Gemfile，内容如下
```bash
source 'https://rubygems.org'      
gem 'github-pages'
```
- 执行 `bundle install`

## 下载主题
- [下载地址](https://github.com/onevcat/vno-jekyll)
## 启动 jekyll
- 在你的 GitHub pages 根目录执行 `bundle exec jekyll serve` 启动 jekyll
- 默认本地预览地址 http://127.0.0.1:4000
- 随时更新 jekyll 可以使用命令 `bundle update`
