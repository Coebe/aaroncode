---
title: The Step of Blog Construction
---

[![Netlify Status](https://api.netlify.com/api/v1/badges/6417f999-72a6-4ebd-994d-0d5118d42bb3/deploy-status)](https://app.netlify.com/sites/sprightly-croquembouche-951681/deploys)  

### Issuse

bug statement:  
`extends includes/layout.pug block content include ./includes/mixins/post-ui.pug #recent-posts.recent-posts +postUI include includes/pagination.pug`
1. 在hexo根目录执行命令：`npm install --save hexo-renderer-jade hexo-generator-feed hexo-generator-sitemap hexo-browsersync hexo-generator-archive`  
2. 清除缓存 `hexo clean`  
3. 重新生成静态文件 `hexo g`/`hexo generate`
