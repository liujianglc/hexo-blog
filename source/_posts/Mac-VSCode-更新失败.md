---
title: Mac VSCode 更新失败
abbrlink: 35092
date: 2019-05-29 22:14:27
tags:
	- Mac
	- VS code
categories: 
	- 工具
---


## Could not create temporary directory: 权限被拒绝

解决方案
```
sudo chown $USER ~/Library/Caches/com.microsoft.VSCode.ShipIt/  
```

重启之后，再更新

