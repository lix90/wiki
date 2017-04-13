---
title: "Git 问题解决"
date: 2017-03-19
tag: git,problem-solving
---

# pull

 问题：**fatal: refusing to merge unrelated histories**
 解决：
 在 merge 时加上 `--allow-unrelated-histories` 选项
 `git pull origin <branch_name> --allow-unrelated-histories`

# Push the master branch into the gh-pages branch

http://stackoverflow.com/questions/20411849/push-local-master-into-gh-pages-branch-on-github
