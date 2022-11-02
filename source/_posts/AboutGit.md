---
title: About Git
cover: https://s2.loli.net/2022/11/02/MPCiJkYKSn3jm4c.png
---

## Problem

![Submodule](https://s2.loli.net/2022/11/02/iRJrgEc4mDWOPUT.png)this image mean has `.git` file in child directory, 然后GitHub就会把这个文件夹视为一个子系统模块,从而不能正常更新Git  

solve step:

1. delete child directory `.git` file.
2. execute `git rm --cached [filename] // filename is the submodule directory`.
3. execute `git add .`.
4. execute `git commit`.
5. execute `git push origin [branchName]`.
