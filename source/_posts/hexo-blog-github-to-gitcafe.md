title: hexo blog 从github切gitcafe | gitcafe 转到 coding
date: 2014-08-29 20:19:29
tags: [heox, github, coding]
---

> 没有用迁移这个说法，这是因为就是重新部署了一下。至于要切过去的原因，我乃天朝子民，岂久用番邦外夷器具乎（i.e. vpn严重影响打开速度）。

gitcafe 帐号开通 gitcafe pages的设置可以google去了。我的blog用的是hexo, 对于git的发布 so so easy，当我迅速的把 repository 和 branch 换掉 发布，悲剧的事情发生了。

1. 无法deploy，把 .deploy 文件夹删掉之后就可以了。
2. push完成页面混乱，在deploy 添加 .nojekyll 文件后页面正常了。

最后说下 hexo blog 数据重复 删掉db.json 即可。

<!--more--> 

##### 2016-03-18 update

最近收到gitcafe合并到coding的消息，又得挪仓库了。gitcafe可以直接把git仓库同步到coding，只需要账号绑定就行。
hexo配置文件中git库地址换成coding的。需要注意一下coding的pages需要绑定默认是coding-pages。