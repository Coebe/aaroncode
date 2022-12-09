---
title: About Git
cover: https://s2.loli.net/2022/11/02/MPCiJkYKSn3jm4c.png
---

## Problem

### Timeout

- **Issue:** *fatal: unable to access 'https://github.com/Coebe/aaroncode.git/': Failed to connect to 192.168.10.120 port 7890 after 21039 ms: Timed out*
- **Fix:**
- **Issue:** *fatal: unable to access 'https://github.com/ThePrimeagen/vim-be-good.git/': Failed to connect to 192.168.10.120 port 7890 after 21080 ms: Timed out*
- **Fix:**
  proxy problem clear that all be fine  
  `git config --global --unset http.xxx`  
  - To set proxy:
    `git config --global http.proxy http://xxx/`
	if needs account & password **don't know meaning**  
	
	`git config --global http.proxy http://user:pwd@ipaddress:port`

### Secure & Authentication

- Add SSH Key over GitHub
  *Key is invalid. You must supply a key in OpenSSH public key format*
  - do not use PRIVATE key, use the `.pub` sub file (under directory: ~/.ssh/)

### Submodule

![Submodule](https://s2.loli.net/2022/11/02/iRJrgEc4mDWOPUT.png)this image mean has `.git` file in child directory, 然后GitHub就会把这个文件夹视为一个子系统模块,从而不能正常更新Git  

solve step:

1. delete child directory `.git` file.
2. execute `git rm --cached [filename] // filename is the submodule directory`.
3. execute `git add .`.
4. execute `git commit`.
5. execute `git push origin [branchName]`.
