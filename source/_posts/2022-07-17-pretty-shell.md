---
layout: post
title: 美化你的终端
subtitle: 受到Tmoe-zsh的启发
author: RuntimeEroor
categories: config
tags: Powershell
date: 2022-07-17
---
# 安装Nerd字体

这个应该没什么难度。

# 安装新款 Powershell Core

[下载地址](https://github.com/PowerShell/PowerShell/releases)

# 安装Powershell插件

```powershell
winget install JanDeDobbeleer.OhMyPosh
Install-Module -Name PSReadLine  -Scope CurrentUser
```

# 配置 PowerShell

在Powershell中输入 `code $PROFILE`打开profile script。
输入以下代码，有注释应该很好懂。

```powershell
#------------------------------- Import Modules BEGIN -------------------------------
# 引入 posh-git
#Import-Module posh-git

# 引入 ps-read-line
Import-Module PSReadLine

# 设置 PowerShell 主题
oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\powerlevel10k_rainbow.omp.json" | Invoke-Expression
#------------------------------- Import Modules END   -------------------------------


#-------------------------------  Set Hot-keys BEGIN  -------------------------------
# 设置预测文本来源为历史记录
Set-PSReadLineOption -PredictionSource History

# 每次回溯输入历史，光标定位于输入内容末尾
Set-PSReadLineOption -HistorySearchCursorMovesToEnd

# 设置向上键为后向搜索历史记录
Set-PSReadLineKeyHandler -Key UpArrow -Function HistorySearchBackward

# 设置向下键为前向搜索历史纪录
Set-PSReadLineKeyHandler -Key DownArrow -Function HistorySearchForward

# 设置 Tab 为菜单补全和 Intellisense
Set-PSReadLineKeyHandler -Key "Tab" -Function MenuComplete

# 回到行首/行尾
Set-PSReadlineKeyHandler -Key "Ctrl+a" -Function BeginningOfLine
Set-PSReadlineKeyHandler -Key "Ctrl+z" -Function EndOfLine

# 前进/后退一个单词
Set-PSReadlineKeyHandler -Key 'Alt+f' -Function ShellForwardWord
Set-PSReadlineKeyHandler -Key 'Alt+b' -Function ShellBackwardWord

# 设置 Ctrl+d 为退出 PowerShell
Set-PSReadlineKeyHandler -Key "Ctrl+d" -Function ViExit

# 设置 Ctrl+z 为撤销
# Set-PSReadLineKeyHandler -Key "Ctrl+z" -Function Undo


# 启用预测性 IntelliSense
Set-PSReadLineOption -PredictionSource History


#-------------------------------  Set Hot-keys END    -------------------------------




#-------------------------------   Set Alias BEGIN    -------------------------------

# 1. 查看目录 ls & ll
function ListDirectory {
	(Get-ChildItem).Name
	Write-Host("")
}
Set-Alias -Name ls -Value ListDirectory
Set-Alias -Name ll -Value Get-ChildItem

# 2. 打开当前工作目录
function OpenCurrentFolder {
	param
	(
		$Path = '.'
	)
	Invoke-Item $Path
}
Set-Alias -Name open -Value OpenCurrentFolder

# 3. 更改工作目录
function Change-Directory {
	param (
		$Path = 'C:\Users\10591\Desktop\'
	)
	Set-Location $Path
}
Set-Alias -Name cd -Value Change-Directory -Option AllScope
#-------------------------------    Set Alias END     -------------------------------
clear
```

# 配置Windows Terminal

```json
"profiles": 
    {
        "defaults": {},
        "list": 
        [
            {
                "closeOnExit": "graceful",
                "colorScheme": "Solarized Dark Higher Contrast",
                "commandline": "C:/Program Files/PowerShell/7/pwsh.exe -nologo",
                "cursorColor": "#FFFFFF",
                "cursorShape": "bar",
                "font": 
                {
                    "face": "Hack Nerd Font",
                    "size": 11
                },
                "guid": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",
                "hidden": false,
                "historySize": 9001,
                "icon": "C:/Program Files/PowerShell/7/assets/Powershell_av_colors.ico",
                "name": "PowerShell 7.2.0",
                "opacity": 100,
                "padding": "5, 5, 20, 25",
                "snapOnInput": true,
                "source": "Windows.Terminal.PowershellCore",
                "startingDirectory": ".",
                "tabTitle": "PowerShell",
                "useAcrylic": false
            },
            {
                "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
                "hidden": false,
                "name": "Windows PowerShell"
            },
            {
                "guid": "{0caa0dad-35be-5f56-a8ff-afceeeaa6101}",
                "hidden": false,
                "name": "Command Prompt"
            },
            {
                "colorScheme": "Campbell",
                "commandline": "C:\\Windows\\system32\\wsl.exe -d Ubuntu-20.04",
                "font": 
                {
                    "face": "Hack Nerd Font"
                },
                "guid": "{4ff38782-a8f1-4767-a657-cdd0c327774f}",
                "hidden": false,
                "icon": "ms-appx:///ProfileIcons/{9acb9455-ca41-5af7-950f-6bca1bc9722f}.png",
                "name": "Ubuntu-20.04",
                "startingDirectory": "~"
            }
        ]
    },
```
