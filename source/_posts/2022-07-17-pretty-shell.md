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
{
    "$help": "https://aka.ms/terminal-documentation",
    "$schema": "https://aka.ms/terminal-profiles-schema",
    "actions": [],
    "copyFormatting": "none",
    "copyOnSelect": false,
    "defaultProfile": "{b453ae62-4e3d-5e58-b989-0a998ec441b9}",
    "keybindings": [
        {
            "id": "Terminal.CopyToClipboard",
            "keys": "ctrl+c"
        },
        {
            "id": "Terminal.FindText",
            "keys": "ctrl+shift+f"
        },
        {
            "id": "Terminal.PasteFromClipboard",
            "keys": "ctrl+v"
        },
        {
            "id": "Terminal.DuplicatePaneAuto",
            "keys": "alt+shift+d"
        }
    ],
    "newTabMenu": [
        {
            "type": "remainingProfiles"
        }
    ],
    "profiles": {
        "defaults": {},
        "list": [
            {
                "font": {
                    "face": "Hack Nerd Font Mono",
                    "size": 12
                },
                "cursorColor": "#FFFFFF",
                "cursorShape": "bar",
                "colorScheme": "Solarized Dark Higher Contrast",
                "commandline": "C:\\Program Files\\PowerShell\\7\\pwsh.exe",
                "guid": "{b453ae62-4e3d-5e58-b989-0a998ec441b9}",
                "hidden": false,
                "name": "PowerShell 7"
            },
            {
                "commandline": "%SystemRoot%\\System32\\WindowsPowerShell\\v1.0\\powershell.exe",
                "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
                "hidden": false,
                "name": "Windows PowerShell"
            },
            {
                "commandline": "%SystemRoot%\\System32\\cmd.exe",
                "guid": "{0caa0dad-35be-5f56-a8ff-afceeeaa6101}",
                "hidden": false,
                "name": "\u547d\u4ee4\u63d0\u793a\u7b26"
            },
            {
                "guid": "{b453ae62-4e3d-5e58-b989-0a998ec441b8}",
                "hidden": false,
                "name": "Azure Cloud Shell",
                "source": "Windows.Terminal.Azure"
            },
            {
                "guid": "{2ece5bfe-50ed-5f3a-ab87-5cd4baafed2b}",
                "hidden": false,
                "name": "Git Bash",
                "source": "Git"
            },
            {
                "guid": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",
                "hidden": false,
                "name": "PowerShell",
                "source": "Windows.Terminal.PowershellCore"
            }
        ]
    },
    "schemes": [
        {
            "background": "#001E27",
            "black": "#002831",
            "blue": "#2176C7",
            "brightBlack": "#006488",
            "brightBlue": "#178EC8",
            "brightCyan": "#00B39E",
            "brightGreen": "#51EF84",
            "brightPurple": "#E24D8E",
            "brightRed": "#F5163B",
            "brightWhite": "#FCF4DC",
            "brightYellow": "#B27E28",
            "cursorColor": "#FFFFFF",
            "cyan": "#259286",
            "foreground": "#9CC2C3",
            "green": "#6CBE6C",
            "name": "Solarized Dark Higher Contrast",
            "purple": "#C61C6F",
            "red": "#D11C24",
            "selectionBackground": "#FFFFFF",
            "white": "#EAE3CB",
            "yellow": "#A57706"
        },
    ],
    "themes": []
}
```