> This HanYajun theme created by [HanYajun](http://www.huweihuang.com/) modified from the original Porter [HuWeihuang](https://github.com/huweihuang/hexo-theme-huweihuang)

# Live Demo

HanYajun Blog : [www.hanyajun.com](http://www.hanyajun.com/)

![Theme HanYajun](http://cdn.hanyajun.com/hanyajun_blog.png)

# Install Hexo

Install Node.js  and Git

```shell
#For Mac
brew install node
brew install git
```

Install hexo

```shell
npm install hexo-cli -g

#For more:https://hexo.io/zh-cn/index.html
```

# Theme Usage

## Init

---
```bash
git clone git@github.com:Han-Ya-Jun/hexo-theme-hanyajun.git ./hexo-hanyajun
cd hexo-huweihuang
npm install
```

## Modify
---
Modify `_config.yml` file with your own info.
Especially the section:
### Deployment
Replace to your own repo!
```yml
deploy:
  type: git
  repo: https://github.com/<yourAccount>/<repo>
  branch: <your-branch>
```

### Sidebar settings
Copy your avatar image to `<root>/img/` and modify the `_config.yml`:
```yml
sidebar: true    # whether or not using Sidebar.
sidebar-about-description: "<your description>"
sidebar-avatar: img/<your avatar path>
```
and activate your personal widget you like
```yml
widgets:         # here are widget you can use, you can comment out
- featured-tags
- short-about
- recent-posts
- friends-blog
- archive
- category
```
if you want to add sidebar widget, please add at `layout/_widget`.
### Signature Setup
Copy your signature image to `<root>/img/signature` and modify the `_config.yml`:
```yml
signature: true   # show signature
signature-img: img/signature/<your-signature-ID>
```
### Go to top icon Setup
My icon is using iron man, you can change to your own icon at `css/image`.

### Post tag
You can decide to show post tags or not.
```yml
home_posts_tag: true
```

![home_posts_tag-true](http://cdn.hanyajun.com/demo.png)
### Markdown render
My markdown render engine plugin is [hexo-renderer-markdown-it](https://github.com/celsomiranda/hexo-renderer-markdown-it).
```yml
# Markdown-it config
## Docs: https://github.com/celsomiranda/hexo-renderer-markdown-it/wiki
markdown:
  render:
    html: true
    xhtmlOut: false
    breaks: true
    linkify: true
    typographer: true
    quotes: '“”‘’'
```
and if you want to change the header anchor 'ℬ', you can go to `layout/post.ejs` to change it.
```javascript
async("https://cdn.bootcss.com/anchor-js/1.1.1/anchor.min.js",function(){
        anchors.options = {
          visible: 'hover',
          placement: 'left',
          icon: ℬ // this is the header anchor "unicode" icon
        };
```

## Hexo Basics
---
Some hexo command:
```bash
hexo new post "<post name>" # you can change post to another layout if you want
hexo clean && hexo generate # generate the static file
hexo server # run hexo in local environment
hexo deploy # hexo will push the static files automatically into the specific branch(gh-pages) of your repo!
```
# Have fun ^_^ 
---
<!-- Place this tag in your head or just before your close body tag. -->
<script async defer src="https://buttons.github.io/buttons.js"></script>
<!-- Place this tag where you want the button to render. -->
Please <a class="github-button" href="https://github.com/Han-Ya-Jun/hexo-theme-hanyajun" data-icon="octicon-star" aria-label="Star huweihuang/hexo-theme-huweihuang on GitHub">Star</a> this Project if you like it! <a class="github-button" href="https://github.com/Han-Ya-Jun" aria-label="Follow @hanyajun on GitHub">Follow</a> would also be appreciated!
Peace!
## 相比原来的版本新增的内容：
- SNS 新增csdn,jianshu等设置，自己修改的话可以直接去修改hexo-theme-hanyajun\themes\huweihuang\layout\_partial（底部图标）hexo-theme-hanyajun\themes\huweihuang\layout\_widget（shout_about图标）
![image](http://cdn.hanyajun.com/demo2.png)
- 新增每日诗词（https://www.jinrishici.com/doc/#json-fast-easy）
 相关文件：hexo-theme-hanyajun\themes\huweihuang\layout\_partial
 ![image](http://cdn.hanyajun.com/demo3.png)

- 如果想插入音乐下载参考这个
https://github.com/MoePlayer/hexo-tag-aplayer
- 原来很多的图片我采用七牛云的cdn了，相比要快很多