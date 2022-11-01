---
title: sth
date: "2022-10-28 18:19:23"
# type: "categories"
---

## This is the first page in categories

what's this?  
I don't know how to use it

## Problem

![Submodule](https://github.com/Coebe/aaroncode/blob/main/source/_posts/src/submodule.jpg) this image mean has `.git` file in child directory, 然后GitHub就会把这个文件夹视为一个子系统模块  

solve step:
1. delete child directory `.git` file.
2. execute `git rm --cached [filename] // filename is the submodule directory`.
3. execute `git add .`.
4. execute `git commit`.
5. execute `git push origin [branchName]`.
