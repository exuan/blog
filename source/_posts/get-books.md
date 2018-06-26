title: books
date: 2018-06-25 21:58:10
tags: [book]
---

> 仓库地址 git@git.coding.net:exuan/geetbook.git

## ssh config
```bash
cat > ~/.ssh/config <<EOF
# geetbook
Host git.coding.net
User coding@mmp
PreferredAuthentications publickey
IdentityFile ~/.ssh/geetbook

EOF
```
<!--more--> 

私钥在群里