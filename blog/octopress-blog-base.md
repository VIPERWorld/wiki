# octopress 博客基本操作

octopress blog基本操作  
http://octopress.org/docs/blogging/

# 安装

gem:
`yum install gem`

bundler:
`gem install bundler`

rake:
`sudo gem install rake`

Could not find rake-0.9.6 in any of the sources
`bundle install`

git clone 项目.
rake等操作

# 新建文章(post)

```bash
#传到博客根目录
cd octopress
#新建日志
rake new_post["Title"]
```

# 预览&发布 

```bash
#在本地预览blog
#转到目录
cd /home/zodiac1111/blog/octopress
#生成
rake generate
#预览 在本地输入 http://localhost:4000/ 访问
rake preview
#发布
rake deploy	
#生成和发布也可以合并成为一句:
rake gen_deploy
```

## 保存source(可选)
```
#保存博客源代码之 页面的source分支下。
cd /home/zodiac1111/blog/octopress
git add .
git commit -m 'blog source update'
#推送至远端
git push origin source
```

# 更新octopress博客程序
```bash
cd octopress
git pull git://github.com/imathis/octopress.git #pull官方程序
```