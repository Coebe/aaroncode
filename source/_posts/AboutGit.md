---
title: About Git
---

## Problem

![Submodule](src/submodule.jpg) this image mean has `.git` file in child directory, 然后GitHub就会把这个文件夹视为一个子系统模块  

solve step:
1. delete child directory `.git` file.
2. execute `git rm --cached [filename] // filename is the submodule directory`.
3. execute `git add .`.
4. execute `git commit`.
5. execute `git push origin [branchName]`.
