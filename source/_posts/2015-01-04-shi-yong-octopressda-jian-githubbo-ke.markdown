---
layout: post
title: "使用octopress搭建github博客"
date: 2015-01-04 11:05:25 +0800
comments: true
thumbnail: /img/2015/06/9.jpg
categories: 
---

<p><a href="http://octopress.org/"><code>Octopress</code></a>是利用<a href="http://github.com/mojombo/jekyll"><code>Jekyll</code></a>博客引擎开发的一个博客系统，生成的静态页面能够很好的在github page上展现。
<!--more-->号称是hacker专属的一个博客系统(<code>A blogging framework for hackers.</code>)</p>

<p>本文只讲自己在苹果电脑(OS X 10.10)利用Octopress搭建一个Github博客,内容参照<code><a href ="http://beyondvincent.com/blog/2013/08/03/108-creating-a-github-blog-using-octopress/">破船之家</a>，<a href="http://blog.devtang.com/blog/2012/02/10/setup-blog-based-on-github/">唐巧_boy</a></code></p>


<h3>目录</h3>

<ul>
<li>1、安装Ruby</li>
<li>2、安装Octopress</li>
<li>3、配置Octopress</li>
<li>4、将博客部署到GitHub上</li>
<li>5、开始写博客</li>
<li>6、更多操作</li>
<li>7、小结</li>
</ul>


<h3>1、安装Ruby</h3>

<p>Octopress需要Ruby环境，RVM(Ruby Version Manager)负责安装和管理Ruby的环境。所以我们先在终端输入如下命令，来安装RVM：</p>

<figure class='code'><div class="highlight"><table><tr><td class="gutter"><pre class="line-numbers"><span class='line-number'>1</span>
</pre></td><td class='code'><pre><code class=''><span class='line'>curl -L https://get.rvm.io | bash -s stable --ruby</span></code></pre></td></tr></table></div></figure>


<p>接着是安装Ruby 1.9.3，在终端依次运行如下命令：</p>

<figure class='code'><div class="highlight"><table><tr><td class="gutter"><pre class="line-numbers"><span class='line-number'>1</span>
<span class='line-number'>2</span>
<span class='line-number'>3</span>
</pre></td><td class='code'><pre><code class=''><span class='line'>rvm install 1.9.3
</span><span class='line'>rvm use 1.9.3
</span><span class='line'>rvm rubygems latest</span></code></pre></td></tr></table></div></figure>


<p>完成上面的操作之后，运行<code>ruby --version</code>应该可以看到ruby 1.9.3环境已经安装好了。🐷：波煮在这里说句，这个ruby version着实让我心塞，搞了好久好久，以至于后来放弃搭建，到现在闲暇之余才努力研究将其解决，具体问题具体谷歌( ⊙ o ⊙ )啊！</p>

<p>参考：<a href="http://octopress.org/docs/setup/rvm/">Installing Ruby With RVM</a></p>

<h3>2、安装Octopress</h3>

<p>在安装Octopress之前，请确保你的电脑上已经安装有git了，在终端输入<code>git --version</code>.

<p>git安装之后，利用git命令将octopress从github上clone到本机，如下命令：</p>

<figure class='code'><div class="highlight"><table><tr><td class="gutter"><pre class="line-numbers"><span class='line-number'>1</span>
<span class='line-number'>2</span>
<span class='line-number'>3</span>
</pre></td><td class='code'><pre><code class=''><span class='line'>git clone git://github.com/imathis/octopress.git octopress
</span><span class='line'>cd octopress    # If you use RVM, You'll be asked if you trust the .rvmrc file (say yes).
</span><span class='line'>ruby --version  # Should report Ruby 1.9.3</span></code></pre></td></tr></table></div></figure>


<p>接着安装相关依赖项：</p>

<figure class='code'><div class="highlight"><table><tr><td class="gutter"><pre class="line-numbers"><span class='line-number'>1</span>
<span class='line-number'>2</span>
<span class='line-number'>3</span>
</pre></td><td class='code'><pre><code class=''><span class='line'>gem install bundler
</span><span class='line'>rbenv rehash    # If you use rbenv, rehash to be able to run the bundle command
</span><span class='line'>bundle install</span></code></pre></td></tr></table></div></figure>


<p>最后安装默认的Octopress 主题。</p>

<figure class='code'><div class="highlight"><table><tr><td class="gutter"><pre class="line-numbers"><span class='line-number'>1</span>
</pre></td><td class='code'><pre><code class=''><span class='line'>rake install</span></code></pre></td></tr></table></div></figure>


<p>参考： <a href="http://octopress.org/docs/setup/">Octopress Setup</a></p>

<h3>3、配置Octopress</h3>

<p>配置<code>_config.yml</code>和<code>Rakefile</code>文件。</p>
其中Rakefile是跟博客部署相关，一般情况下并不需要修改这个文件，除非使用了rsync。</p>

<p><em>config.yml是博客重要的一个配置文件，在</em>config.yml文件中有三大配置项：<code>Main Configs</code>、<code>Jekyll &amp; Plugins</code>和<code>3rd Party Settings</code>。</p>

<p>一般，该文件中其中<code>url</code>是必须要填写的，这里的url是在github上创建的一个仓库地址，具体请看第四步中创建的地址。另外再修改一下<code>title</code>、<code>subtitle</code>和<code>author</code>，根据需求，在开启一些第三方组件服务。</p>

<b><code>再注：</code>波煮将在下篇文章中说明一些搭建之后在拥有全球超级局域网的天朝的一些令人心塞令人烦闷的墙内话</b></p>

<p>关于_config.yml文件中的更多内容，请看这里的内容：<a href="http://octopress.org/docs/configuring/">Configuring Octopress</a></p>

<h3>4、将博客部署到GitHub上</h3>

<p>Github的<a href="http://pages.github.com/"><code>Page service</code></a>可以免费托管博客，并且还可以自定义域名。</p>

<p>首先需要在GitHub上<a href="https://github.com/new"><code>创建一个仓库</code></a>，并将仓库名称按照这样的方式进行命名：<code>username.github.com</code>或<code>organization.github.com</code>。等后面配置完毕之后，我们就可以在浏览器中使用页面地址<code>http://username.github.com</code>来访问我们的博客。一般来说，我们希望在将博客的源码放到source分支下，并把生成的内容提交到master分支。</p>

<p>创建好仓库之后，我们需要利用octopress的一个<code>配置rake任务</code>来自动配置上面创建的仓库：可以让我们方便的部署GitHub page。在终端输入如下命令：</p>

<figure class='code'><div class="highlight"><table><tr><td class="gutter"><pre class="line-numbers"><span class='line-number'>1</span>
</pre></td><td class='code'><pre><code class=''><span class='line'>$ rake setup_github_pages</span></code></pre></td></tr></table></div></figure>


<p>上面的命令会做一些事情(详细介绍看下面给出的参考链接)。其中最主要的就是创建一个<code>_deploy</code>目录，目录用来存放部署到master分支的内容。期间会要求你输入仓库的url，根据提示，进行输入即可。</p>

<p>完成上面的命令之后，我们就可以生成博客并真正的部署到仓库中了。执行如下命令：</p>

<figure class='code'><div class="highlight"><table><tr><td class="gutter"><pre class="line-numbers"><span class='line-number'>1</span>
<span class='line-number'>2</span>
</pre></td><td class='code'><pre><code class=''><span class='line'>rake generate
</span><span class='line'>rake deploy</span></code></pre></td></tr></table></div></figure>


<p>上面的命令首先生成博客文件，并将生成的博客文件拷贝到<code>_deploy/</code>目录下，然后将这些内容添加到git中，并commit和push到仓库的master分支。</p>

<p>现在可以访问<code>http://username.github.com</code>了。注意：有时候可能会有延时，要等几分钟才能打开。</p>

<p>至此，我们的博客已经完成基本的部署，不过博客的source需要单独提交，执行如下命令就可以将source提交到仓库的source分支下。</p>

<figure class='code'><div class="highlight"><table><tr><td class="gutter"><pre class="line-numbers"><span class='line-number'>1</span>
<span class='line-number'>2</span>
<span class='line-number'>3</span>
</pre></td><td class='code'><pre><code class=''><span class='line'>$ git add .
</span><span class='line'>$ git commit -m 'Initial source commit'
</span><span class='line'>$ git push origin source</span></code></pre></td></tr></table></div></figure>


<p>如果在部署到仓库之前，需要先预览一下博客，可以在终端输入<code>rake preview</code>命令，然后就能在浏览器中进行本地预览访问了：<code>http://127.0.0.1:4000/</code>或<code>http://localhost:4000/</code>，效果跟仓库中的一样。</p>

<p>参考：<a href="http://octopress.org/docs/deploying/">Deploying to Github Pages</a></p>

<h3>5、开始写博客</h3>

<p>Octopress为我们提供了一些task来创建博文和页面。博文必须存储在<code>source/_posts</code>目录下，并且需要按照Jekyll的命名规范对文章进行命名：<code>YYYY-MM-DD-post-title.markdown</code>。文章的名字会被当做url的一部分，而其中的日期用于对博文的区分和排序。</p>

<p>通过Octopress提供的task可以正确的按照命名规范创建一个博文，并且在博文中会附带常用的一些yaml元数据。只需要在终端输入如下命令：</p>

<figure class='code'><div class="highlight"><table><tr><td class="gutter"><pre class="line-numbers"><span class='line-number'>1</span>
</pre></td><td class='code'><pre><code class=''><span class='line'>rake new_post["title"]</span></code></pre></td></tr></table></div></figure>


<p>其中title为博文的文件名，创建出来的文件默认是markdown格式。上面的命令会创建出这样一个文件：<code>source/_posts/2013-08-03-title.markdown</code>。打开这个文件，可以看到里面有如下一些内容了(告诉Jekyll博客引擎如何处理博文和页面)：</p>

<figure class='code'><div class="highlight"><table><tr><td class="gutter"><pre class="line-numbers"><span class='line-number'>1</span>
<span class='line-number'>2</span>
<span class='line-number'>3</span>
<span class='line-number'>4</span>
<span class='line-number'>5</span>
<span class='line-number'>6</span>
<span class='line-number'>7</span>
</pre></td><td class='code'><pre><code class=''><span class='line'>---
</span><span class='line'>layout: post
</span><span class='line'>title: "title"
</span><span class='line'>date: 2013-08-03 16:36
</span><span class='line'>comments: true
</span><span class='line'>categories: 
</span><span class='line'>---</span></code></pre></td></tr></table></div></figure>


<p>接着我们就可以在这个文件中写我们的博文啦。完成之后，我们可以预览和部署博文。下面是创建并部署博文的一个完整过程：</p>

<figure class='code'><div class="highlight"><table><tr><td class="gutter"><pre class="line-numbers"><span class='line-number'>1</span>
<span class='line-number'>2</span>
<span class='line-number'>3</span>
<span class='line-number'>4</span>
<span class='line-number'>5</span>
<span class='line-number'>6</span>
</pre></td><td class='code'><pre><code class=''><span class='line'>$ rake new_post["New Post"]
</span><span class='line'>$ rake generate
</span><span class='line'>$ git add .
</span><span class='line'>$ git commit -am "Some comment here." 
</span><span class='line'>$ git push origin source
</span><span class='line'>$ rake deploy</span></code></pre></td></tr></table></div></figure>


<p>参考：<a href="http://octopress.org/docs/blogging/">Blogging Basics</a></p>

<h3>6、后续</h3>

<p>在搭建博客后，你会发现打开很慢很慢，所以我们需要对其做一个优化，这些内容写在另外一篇文章中，<a href="http://langyapojun.github.io/blog/2015/01/04/jie-jue-octopressfang-wen-man-he-%5B%3F%5D-xie-she-zhi-wen-ti/"><code>跳吧，年轻人</code></a>。</p>