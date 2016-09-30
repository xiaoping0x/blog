---
layout: post
title: Jekyll up and running
---

Jekyll是比较完善的静态站点生成器，有很多的插件和主题可以选择，尤其是Github的Pages深度支持Jekyll，依赖于Github强大的服务器，可以很轻松的创建一个博客站点。

如果是初次使用Jekyll，建议查看Jekyll[官方文档](https://jekyllrb.com)，官方文档比较全面，可以很快的上手。

这里简单的介绍一下在Mac下面如何来安装和运行Jekyll：

```sh
# 1. install jekyll
#    国内用户如果网速慢，可以将source修改为https://ruby.taobao.org/
#    如果发布的时候最好还是修改回默认的，因为Github需要用默认的
gem install jekyll
gem install bundle

# 2. create new site, using --force if folder is not empty
jekyll new .

# 3. install gems
bundle install

# 4. build
jekyll build

# 5. serve and visit http://localhost:4000
#    -w 监听文件变化自动增量编译，但是如果修改了_config文件，需要手动重启
jekyll serve . -w
```

## 选择主题

默认使用的[minima](https://github.com/jekyll/minima)主题，但是主题比较简单，而且是英文版本，所以我们需要定制或者找一些比较完善的主题。

我发现Bootstrap的创始人[@mdo](https://github.com/mdo)开发了2个响应式的主题[hyde](https://github.com/poole/hyde)和[lanyon](https://github.com/poole/lanyon)都比较好，所以我最终选择了hyde主题。

_因为我使用的Jekyll比较新的版本，而hyde是基于旧版本开发，所以我需要根据新版本的变化来移植，而且因为hyde也是英文版本，所以我仍然需要定制为中文版本。万能的Github，我找到一个国人基于Hyde定制的支持Jekyll V3的主题[Hyde-for-jekyll-3](https://github.com/jeromechan)。基于他定制后的主题，我修改了一下中文，就可以使用了。_

## 选择插件

### 优化流程
刚开始使用Jekyll觉得比较疑惑的就是，页面的名称必须包含日期和标题，但是没有一个命令可以快速创建一个页面的。后来发现Jekyll自己就开发了一个[jekyll-compose](https://github.com/jekyll/jekyll-compose)插件，增加了几个命令可以优化编辑流程。

安装插件需要使用Gemfile，因此我增加了一个Gemfile文件，增加对`jekyll-compose`的依赖：

```ruby
gem 'jekyll-compose', group: :jekyll_plugins
```

_增加了这个后，启动jekyll需要使用`bundle exec jekyll serve . -w`才行，不然会报错。_

安装好这个插件后就可以使用如下命令：

```sh
  bundle exec jekyll draft      # Creates a new draft post with the given NAME
  bundle exec jekyll post       # Creates a new post with the given NAME
  bundle exec jekyll publish    # Moves a draft into the _posts directory and sets the date
  bundle exec jekyll unpublish  # Moves a post back into the _drafts directory
  bundle exec jekyll page       # Creates a new page with the given NAME
```

## 部署到Github Pages

将代码提交到master或者gh-pages分支后，很快就可以看到自己的博客了。

