---
layout: post
title: Conda for Powershell 7
subtitle: 初试 AI 绘画最艰难的一环居然是……
author: RuntimeEroor
categories: config
tags: [Conda, Powershell] 
date: 2025-01-27
---
# 1. 问题描述

[Fail to initialize conda in latest PowerShell Preview](https://github.com/conda/conda/issues/14237)

# 2. 解决方案

[On Powershell 7.5 preview 4, after conda activate base, Env:_CE_CONDA and Env:_CE_M appears again. ](https://github.com/conda/conda/issues/14292)

1. 修改 Powershell Profile，添加 `$Env:_CE_M = $null $Env:_CE_CONDA = $null`
2. 修改 Conda.psm1，替换 `Invoke-Conda`函数
   ```powershell
   function Invoke-Conda() {
       # Don't use any explicit args here, we'll use $args and tab completion
       # so that we can capture everything, INCLUDING short options (e.g. -n).
       if ($Args.Count -eq 0) {
           # No args, just call the underlying conda executable.
           & $Env:CONDA_EXE $Env:_CE_M $Env:_CE_CONDA;
       }
       else {
           $Command = $Args[0];
           if ($Args.Count -ge 2) {
               $OtherArgs = $Args[1..($Args.Count - 1)];
           } else {
               $OtherArgs = @();
           }
           switch ($Command) {
               "activate" {
                   Enter-CondaEnvironment @OtherArgs;
                   $Env:_CE_M = $null; $Env:_CE_CONDA = $null;
               }
               "deactivate" {
                   Exit-CondaEnvironment;
                   $Env:_CE_M = $null; $Env:_CE_CONDA = $null;
               }

               default {
                   # There may be a command we don't know want to handle
                   # differently in the shell wrapper, pass it through
                   # verbatim.
                   & $Env:CONDA_EXE $Env:_CE_M $Env:_CE_CONDA $Command @OtherArgs;
               }
           }
       }
   }
   ```
