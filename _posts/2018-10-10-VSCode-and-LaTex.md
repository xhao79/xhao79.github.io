---
layout: default
title: 使用VSCode编写LaTeX
date: 2018-10-10
author: HAO Xuguang
---

<h1>{{ page.title }}</h1>
<p>{{ page.author }}</p>
<p>{{ page.date }}</p>


<!-- TOC -->

- [1. Installation](#1-installation)
- [2. Configure](#2-configure)

<!-- /TOC -->


使用VSCode编写简单的文档以及设置外部PDF阅读器的方法。
It has referred to following articles:
- [使用VSCode编写LaTeX](https://zhuanlan.zhihu.com/p/38178015)


# 1. Installation

- Textlive
- LaTex Workshop for VSCode


# 2. Configure

将以下代码放入 VSCode 的设置文件 _settings.json_ 中, _settings.json_ 文件位于 `~/.config/Code/User/`.

- **Compiling Tools**

    _LaTeX Workshop_ 默认的编译工具是 `latexmk`.
    把其修改为中文环境最常用的 `xelatex`.

    ```
    "latex-workshop.latex.tools": [
        {
            // 编译工具和命令
            "name": "xelatex",
            "command": "xelatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-pdf",
                "%DOC%"
            ]
        },
        {
            "name": "pdflatex",
            "command": "pdflatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "%DOC%"
            ]
        },
        {
            "name": "bibtex",
            "command": "bibtex",
            "args": [
                "%DOCFILE%"
            ]
        }
    ],
    ```

- **Recipes**

    配置编译链.
    第一个 recipe 为默认的编译工具.
    如需要使用 `bibtex` 可在编译时单击 VSCode 界面左下角的小勾, 单击 **Build LaTeX project**, 选择 **xe->bib->xe->xe**, 或者直接将 **xe->bib->xe->xe** 的 recipe 放到第一位, 即可以默认工具编译, 但会比较慢.

    ```
    "latex-workshop.latex.recipes": [
        {
            "name": "xelatex",
            "tools": [
                "xelatex"
            ]
        },
        {
            "name": "xe->bib->xe->xe",
            "tools": [
                "xelatex",
                "bibtex",
                "xelatex",
                "xelatex"
            ]
        }
    ],
    ```

- **Special Statement**

    在编写 LaTeX 文档时, 有两个特殊的命令:
    - `%!TEX program` 用于指定编译当前 TeX 文档所用的命令, 例如: `%!TEX program = xelatex`. 这个命令只接受一个命令名字符串.
    - `%!TEX root` 用于指定主(根)文件, 例如 `%!TEX root = relative/or/absolute/path/to/root/file.tex`


- **External PDF Viwer**

    以 Windows 下的 SumatraPDF 为例, 要使用外部PDF浏览器预览编译好的PDF文件, 添加以下代码进入 VSCode 设置区.
    ```
    "latex-workshop.view.pdf.viewer": "external",

    "latex-workshop.view.pdf.external.command": {
        "command": "E:/Programs/SumatraPDF/SumatraPDF.exe",
        "args": [
            "%PDF%"
        ]
    },
    ```
    - _viewer_ 设置阅读器为外置阅读器.
    - _command_ 为 SumatraPDF.exe 的路径, 根据具体情况修改。
    - _%PDF%_ 为预编译结果文件的文件名

- **Search forward**

    仍以 SumatraPDF 为例, 使用外部PDF浏览器 _正向搜索_, 添加以下代码进入 VSCode 设置区.

    ```
    "latex-workshop.view.pdf.external.synctex": {
        "command": "E:/Programs/SumatraPDF/SumatraPDF.exe",
        "args": [
            "-forward-search",
            "%TEX%",
            "%LINE%",
            "%PDF%"
        ]
    },
    ```
    _command_ 依旧是SumatraPDF.exe的存放位置，根据具体情况修改。

- **Search backward**

    以 SumatraPDF 为例, 使用外部PDF浏览器 _反向搜索_, 在 SumatraPDF 的设置中 _请键入双击PDF文件时, 应运行的命令(E):_

    ```
    E:/Programs/SumatraPDF/SumatraPDF.exe -g "%f:%l"
    ```

- **Build when Saving**

    LaTeX Workshop 默认保存的时候编译

    ```
    "latex-workshop.latex.autoBuild.onSave.enabled": false,
    ```

- 