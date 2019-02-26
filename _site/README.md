# wlacp.github.io
博客

## 本地调试
- 确保你的ruby --version为 1.9.3 or 2.0.0 (if not,pls google by yourself to install ruby with right version)
- 安装bundler包管理器 sudo gem install bundler
- 在你的site(github-page) 主目录下创建Gemfile,该文件内的具体内容如下:
```code
source 'https://rubygems.org'      
gem 'github-pages'
```
- 执行bundle install
- 以上你就已经顺利的在本地安装好了与github-page对应的版本的jekyll，之后你需要做的就是在你的site根目录下执行bundle exec jekyll serve启动jekyll，默认访问地址为：http://localhost:4000，这样你就顺利的得到了一个本地版的github-page镜像:)

- 最后你可以随时更新你本地的jekyll，通过bundle update。
