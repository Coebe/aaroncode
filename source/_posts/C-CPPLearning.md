---
title: C-CPPLearning
date: 2023-01-03 11:55:54
tags:
cover: https://github.com/Coebe/aaroncode/blob/main/source/_posts/src/C-CPPLearning.png?raw=true
---

## Data Type

### Convert

- string to int
  bacause `atoi()` is C base function, and the parameter is char array  
  so firt step is convert `string` to `char[]`, and then..
  - `int num = atoi(str.c_str());`
