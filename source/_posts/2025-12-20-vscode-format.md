---
title: Visual Studio Code 格式化
date: 2025-12-20 16:55:50
tags: VSCode
categories: 开发环境配置
toc: true
excerpt: Visual Studio Code 格式化相关配置
---
# 安装插件
## Doxygen Documentation Generator
在Doxygen Documentation Generator设置中打开`settings.json`,添加以下配置：
```bash
{
    "editor.formatOnPaste": true,
    "editor.formatOnSave": true,
    "C_Cpp.clang_format_fallbackStyle": "Google",
    "C_Cpp.formatting": "vcFormat",
    "C_Cpp.vcFormat.newLine.beforeOpenBrace.block": "sameLine",
    "C_Cpp.vcFormat.newLine.beforeOpenBrace.function": "sameLine",
    "C_Cpp.vcFormat.newLine.beforeOpenBrace.lambda": "sameLine",
    "C_Cpp.vcFormat.newLine.beforeOpenBrace.namespace": "sameLine",
    "C_Cpp.vcFormat.newLine.beforeOpenBrace.type": "sameLine",
    "C_Cpp.vcFormat.indent.preserveComments": true,
    "doxdocgen.file.fileOrder": [
        "file",
        "author",
        "brief",
        "version",
        "date",
        "empty",
        "copyright"
    ],
    "doxdocgen.file.fileTemplate": "@file        path/{name}",
    "doxdocgen.generic.authorTag": "@author      wen",
    "doxdocgen.file.versionTag": "@version     0.1.0",
    "doxdocgen.generic.dateTemplate": "@date        {date}",
    "doxdocgen.file.copyrightTag": [
        "@copyright   Copyright (c) {year}"
    ],
}
```