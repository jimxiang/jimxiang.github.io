title: "How to build your owner blog with HEXO"   
date: 2015-04-18 18:25:01    
tags: Hexo | Blog
---

### 今天真高兴，涨了不少姿势。   
1.学会了使用Hexo搭建一个静态博客   
2.学会了使用MarkDown这种简单的标记语言编写文章   

前几天看到学长在用MarkDown写博客，感觉逼格很高，程序员风格十足。今天终于入门了，现把一些主要步骤记录一下   

1.首先要有一个[github](https://github.com)账号，然后建立一个repository(仓库)，关键点在于 **仓库名称要与你的账号名称相同，并在后面加上github.io**   
例如: 我的github叫做 **jimxiang**,那么就建一个名为 **jimxiang.github.io**的仓库。接下来要配置SSH,网上教程很多，这里不再赘述。**   

2.使用node.js里的npm在命令行里进行接下来的操作   

### 安装Hexo
<pre><code> $ npm install -g hexo // -g  表示把hexo安装到全局，不限于当前文件夹，以后重建项目时不必再次安装</code></pre>

### 部署Hexo
<pre><code> $ hexo init </code></pre>   
现在已经搭建好本地的hexo博客了，执行以下命令   
<pre><code> $ hexo g   // 生成静态页面至public目录</code></pre>
<pre><code> $ hexo s   // 开启预览访问端口（默认端口4000，'ctrl + c'关闭server）</code></pre>

### 到浏览器输入 **localhost:4000** 看看

### 更换博客主题
github上有许多[博客主题](https://github.com/hexojs/hexo/wiki/Themes)。现在clone一个你最喜欢的主题   
<pre><code> $ git clone https://github.com/...(主题地址)</code></pre>

### 例如
<pre><code> $ git clone https://github.com/wuchong/jacman.git themes/jacman</code></pre>

### 启用主题
修改Hexo目录下的config.yml配置文件中的theme属性，将其设置为jacman。   
<pre><code> theme: jacman</code></pre>

**注意：Hexo有两个config.yml文件，一个在根目录，一个在theme下，此时修改的是在根目录下的。**

### 更新主题
<pre><code> $ cd themes/jacman</code></pre>   
<pre><code> $ git pull</code></pre>

### 使用与调试
启动本地服务，实时查看你的blog   
<pre><code> $ hexo serve</code></pre>

### 到了重要的一步：把本地的博客部署到github上（有木有很激动）
配置 **根目录下的config.yml** 文件   
<pre><code> deploy:</code></pre>   
<pre><code> type: git</code></pre>   
<pre><code> repository: git@github.com/...(你自己的github地址)</code></pre>
<pre><code> branch: master</code></pre>

### npm命令
<pre><code> $ hexo clean</code></pre>   
<pre><code> $ hexo generate</code></pre>   
<pre><code> $ hexo deploy  //这一步会让你输入你的github用户名和密码</code></pre>

### 到此为止，你可以登陆 **xxx.github.io** 查看你的博客啦!

### Hexo修改blog主页内容：
修改根目录下的 **config.yml** 文件

### 新建文章
<pre><code>$ hexo new "（文章名）" //新建一个xxx.md的文件</code></pre>   
使用 **记事本、sublime text、chrome插件** 等编辑 *source/_posts文件下的.md* 文件，借助[MakeDown](http://www.markdown.cn/)语言写入你的文章

### 写完后，推送到服务器上
<pre><code> $ hexo g</code></pre>   
<pre><code> $ hexo d</code></pre>

现在我们完成了用Hexo和github建立静态博客，是不是很有趣呢？赶紧动手吧！
