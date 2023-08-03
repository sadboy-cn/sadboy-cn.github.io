---
title: Shell命令记录
date: 2021-4-25 15:35:33 +0800
categories: [学习, Shell]
tags: [study, Shell]     # TAG names should always be lowercase
---

## 1、shell结果赋值变量

>pwd 的输出被赋给变量 currPath，打印currPath，创建bin目录

```shell
currPath=$(pwd) 或 $ currPath=`pwd`
echo $currPath
mkdir $currPath/bin
```
