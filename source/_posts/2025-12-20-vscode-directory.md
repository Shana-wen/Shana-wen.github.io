---
title: 在右键菜单中添加Visual Studio Code
date: 2025-12-20 15:18:04
tags: VSCode
categories: 开发环境配置
toc: true
excerpt: 修改Win10注册表，实现在右键菜单中添加Visual Studio Code
---
# Win10 在右键菜单中添加Visual Studio Code
1. `Win+R`，输入`regedit`，打开注册表。
- 导航到`HKEY_CLASSES_ROOT\Directory\shell`。
2. 新建项，可命名为`VS Code`，可将其(默认)数值的数据改为`Open VS Code here`。
3. 选择`VS Code`项，新建字符串值，命名为`Icon`,数据改为`E:\Program Files\Microsoft VS Code\resources\app\extensions\microsoft-authentication\media\favicon.ico`,其为VS Code图标路径。
4. 在`VS Code`项下，新建`command`项，修改其(默认)数值的数据为`"E:\Program Files\Microsoft VS Code\Code.exe" "%V"`。`%V`代表当前右键单击的路径
5. 导航到`HKEY_CLASSES_ROOT\Directory\Background\shell`，同上修改。