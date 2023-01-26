---
layout: post
title:  "Jekyll与GitHub pages建站"
date:   2023-01-24 18:34:52 +0800
categories: jekyll update
---
## 创建GitHub pages

------

搭建自己的博客，朴素的想法是租借一台服务器从零配置。这里使用GitHub pages，优点包括：

-   免费
-   即使不懂技术细节，也只需按步骤一步步操作即可
-   支持的功能多，玩法丰富，你可以绑定你的域名、使用免费的 HTTPS、自己 DIY 网站的主题、使用他人开发好的插件等等
-   当完成搭建后，只需要专注于文章创作，其他诸如环境搭建、系统维护、文件存储的事情一概不用操心，都由 GitHub 处理

创建流程：

1.   默认你已经拥有**GitHub**账号
2.   创建一个新的 public repository， 名字为 `[你的GitHub账号名].github.io`，这也是你网站的初始网址
3.   将仓库克隆到本地，添加一个`index.html`，里面随便写点什么，push到远程仓库
4.   浏览器访问`[你的GitHub账号名].github.io`，你能看到你写的`index.html`啦！

>   GitHub pages官网以及简单流程：https://pages.github.com/
>
>   某个GitHub Pages 搭建教程：https://sspai.com/post/54608

## 使用Jekyll

------

你已经拥有自己的网站了，朴素的想法是从零开始编写HTML，CSS与JavaScript文件。~~但是我太菜了~~

如果想快速实现好看的页面呢？可以考虑使用**Jekyll**，这也是GitHub官方推荐的。

>   Jekyll 是一个静态站点生成器，内置 GitHub Pages 支持和简化的构建过程。 Jekyll 使用 Markdown 和 HTML 文件，并根据您选择的布局创建完整静态网站。 
>
>   来自GitHub文档：https://docs.github.com/zh/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll

了解了Jekyll之后，让我们正式开始吧。

>   注意，博主的电脑为Mac，以下内容来源：
>
>   -   Jekyll官网文档：https://jekyllrb.com/docs/
>   -   某个Mac安装Jekyll的教程：https://blog.csdn.net/wanghao_sh/article/details/128196126

### 安装依赖

-   [GCC](https://gcc.gnu.org/install/)。执行 `gcc -v`,`g++ -v` 检查
-   [Make](https://www.gnu.org/software/make/)。执行`make -v` 检查
-   [Ruby](https://www.ruby-lang.org/en/downloads/)  **2.5.0** 或更高版本。执行`ruby -v`检查
-   [RubyGems](https://rubygems.org/pages/download) 。执行`gem -v`检查

>   说明：Jekyll 的本质是一个Ruby Gem组件，使用Ruby编写，所以需要相关依赖。
>
>   对Ruby一窍不通？看看这两个介绍视频/文档：
>
>   -   【熟肉】100秒介绍Ruby【Fireship】：https://www.bilibili.com/video/BV1PU4y1z7Fs/
>   -   Ruby 101：https://jekyllrb.com/docs/ruby-101/

#### 安装Homebrew

为了安装**Ruby**，在Mac上首先推荐安装**Homebrew**。Homebrew是一款Mac OS平台下的软件包管理工具，安装软件而不用关心各种依赖和文件路径的情况，十分方便快捷。

在使用brew安装软件时, 经常会报错 failed to connect to [http://raw.githubusercontent.com](https://link.zhihu.com/?target=http%3A//raw.githubusercontent.com) port 443, 出现的原因是DNS污染，推荐Mac安装brew的命令：

```
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```

>   原文：https://zhuanlan.zhihu.com/p/111014448

>   几个brew命令
>
>   -   本地软件库列表：`brew ls`
>   -   查找软件：`brew search [关键字]`
>   -   查看brew版本：`brew -v `
>   -   更新brew版本：`brew update`
>   -   安装cask软件：`brew install --cask [软件]`

使用命令安装完brew后显示warning：

```
Warning: No remote 'origin' in /usr/local/Homebrew/Library/Taps/homebrew/homebrew-cask, skipping update and reset!
Warning: No remote 'origin' in /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core, skipping update and reset!
Warning: No remote 'origin' in /usr/local/Homebrew/Library/Taps/homebrew/homebrew-services, skipping update and reset!
```

不过后面马上有解决方法，把命令运行一下就行：

```
fatal: unsafe repository ('/usr/local/Homebrew/Library/Taps/homebrew/homebrew-core' is owned by someone else)
To add an exception for this directory, call:

	git config --global --add safe.directory /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core
Homebrew/homebrew-core (no Git repository)
```

#### 安装Ruby

安装：

```
brew install ruby
```

切换版本与设置，可能要使用管理员权限：

```
echo 'export PATH="/usr/local/opt/ruby/bin:$PATH"' >> ~/.zshrc
export LDFLAGS="-L/usr/local/opt/ruby/lib"
export CPPFLAGS="-I/usr/local/opt/ruby/include"
```

重进一下终端，查看Ruby版本：

```
ruby -v
```

显示`ruby 3.2.0 (2022-12-25 revision a528908271) [x86_64-darwin21]`，安装完成。

### 安装与配置Jekyll

1. 安装Jekyll：

```
gem install jekyll
```

2. 安装bundler（功能类似Make）：

```
gem install jekyll bundler
```

3. 在 `./myblog` 目录下创建一个全新的Jekyll网站：

```
jekyll new myblog
```

4. 进入新创建的目录：

```
cd myblog
```

5. 构建网站并启动一个本地web服务：

```
 bundle exec jekyll serve
```

6.   在浏览器上打开网址`http://127.0.0.1:4000/`，你能看到初始的网页啦！

