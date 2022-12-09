---
title: The Step of Blog Construction
date: "2022-10-10 17:40:08"
cover: https://s2.loli.net/2022/12/09/16jNOPTasK8VM4X.png
---

### Reference

[![Netlify Status](https://api.netlify.com/api/v1/badges/6417f999-72a6-4ebd-994d-0d5118d42bb3/deploy-status)](https://app.netlify.com/sites/sprightly-croquembouche-951681/deploys)  

### Issuse

### About Connexity ~连通性问题~

bug statement:  
打开网站`HTTP ERROR 502`  

solution:  
原因是访问不到Hexo所指的服务, 也就是代理出现了问题, 查看Cloudflare DNS配置,并修改成 CNAME 模式(通过 Cloudflare 转发 [aaroncode].netlify.app)

#### About Cache ~缓存问题~

bug statement:  
> extends includes/layout.pug block content include ./includes/mixins/post-ui.pug #recent-posts.recent-posts +postUI include includes/pagination.pug

solution:  
1. 在hexo根目录执行命令：
`npm install --save hexo-renderer-jade hexo-generator-feed hexo-generator-sitemap hexo-browsersync hexo-generator-archive`  
2. 清除缓存
`hexo clean`  
3. 重新生成静态文件
`hexo g`/`hexo generate`

```C++
code block example
```
