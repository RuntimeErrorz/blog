---
layout: post
title: Overleaf 增强版本地部署
subtitle: 用了之后感觉之前在浪费时间
author: RuntimeEroor
categories: 工具
tags: [LaTeX, Overleaf] 
date: 2025-11-06
---

# 1. Overleaf Toolkit 安装与初始化

使用官方提供的 Toolkit 脚本来管理 Docker 容器。

## 1.1 获取 Toolkit 代码
```bash
git clone --depth=1 https://github.com/overleaf/toolkit.git ./overleaf-toolkit
cd overleaf-toolkit
```

## 1.2 初始化配置
生成默认的配置文件（`config/overleaf.rc`, `config/variables.env` 等）。
```bash
bin/init
```

## 1.3 替换为 CEP 镜像 (关键步骤)
原版 Toolkit 默认使用官方 CE 镜像。为了使用增强版（CEP），需要手动拉取第三方镜像并修改配置。

**拉取镜像：**
```bash
# 尝试拉取 overleaf-cep 镜像
docker pull overleafcep/sharelatex:5.5.3-ext-v3.1
```

**修改配置：**
编辑 `docker-compose.override.yml` 或 `config/overleaf.rc`，将镜像指向 `overleafcep/sharelatex:ext-ce`。

---

# 2. 服务启动与调试

## 2.1 首次启动
```bash
# 启动服务 (-d 后台运行)
bin/up -d

# 检查服务状态
bin/doctor
```
---

# 3. 高级定制：集成 Inkscape 与 TeX Live Full 并构建新镜像

为了支持 SVG 转换等功能以及完整的 LaTeX 宏包支持，您在容器内安装了 Inkscape 和 TeX Live Full，并将其保存为新的 Docker 镜像。

## 3.1 进入容器安装软件
```bash
# 进入 ShareLaTeX 容器的 Shell
bin/shell

# (在容器内部) 1. 安装 Inkscape
# 更新包列表并安装
apt-get update
apt-get install -y inkscape
# 验证安装
inkscape --version

# (在容器内部) 2. 安装 TeX Live Full (升级到完整版)
# 默认镜像可能只包含基础包，安装 scheme-full 以支持所有宏包
# 注意：此过程下载量大，耗时较长
tlmgr option repository [镜像站地址]
tlmgr update --self
tlmgr install scheme-full
```

## 3.2 提交自定义镜像 (Docker Commit)
将安装好环境的容器保存为新的镜像，防止重启后丢失更改。

```bash
# 1. 停止服务
bin/stop

# 2. 找到容器 ID 或名称 (通常是 sharelatex)
docker ps -a --filter name=sharelatex

# 3. 提交新镜像
# 命名格式：overleafcep/sharelatex:<版本>-<特性>
docker commit sharelatex overleafcep/sharelatex:5.5.3-ext-v3.1-tlfull-inkscape

# 4. 验证镜像是否创建成功
docker images
```

---

# 4. 最终部署与维护

使用自定义构建的镜像进行最终部署。

## 4.1 更新配置使用新镜像
修改 `overleaf-toolkit` 中的配置，将 `OVERLEAF_IMAGE_NAME` 指向刚才 commit 的新镜像：
`overleafcep/sharelatex:5.5.3-ext-v3.1-tlfull-inkscape`

## 4.2 重启服务
```bash
bin/up -d
```

## 4.3 常用维护命令
```bash
# 停止服务
bin/stop

# 启动服务
bin/start

# 查看日志 (排查 502 错误等)
# 进入容器调试
bin/shell
```