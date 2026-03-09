---
title: BenD渗透测试工具箱
date: 2026-03-09 11:11:38
tags:
    - 安全工具
cover:https://files.seeusercontent.com/2026/03/09/me2Z/Attack-911.png
top_img:https://files.seeusercontent.com/2026/03/09/me2Z/Attack-911.png
---

注：本工具箱基于One-Fox工具箱改编而来，采用他的ui和管理方法，如若侵权可联系我删除
# BenD 渗透测试工具箱使用方法
直接双击BenD渗透测试工具箱.vbs即可启动

# BenD 渗透测试工具箱展示截图

![image-20260309094022882](https://files.seeusercontent.com/2026/03/09/9eRo/image-20260309094022882.png)

# BenD 渗透测试工具箱


一个基于 PyQt6 的本地渗透测试工具集启动器与管理器，聚合常用的信息收集、漏洞扫描、后渗透、免杀、抓包代理、WebShell 管理及网页工具，支持分类管理、模糊搜索、快捷键与主题配置，开箱即用。

## 功能概览

- 图形化工具管理：按分类展示，支持添加/编辑/删除工具
- 统一启动方式：支持 GUI、命令行、Python、批处理、PowerShell、Java 8/11、网页
- 模糊搜索与权重排序：快速定位常用工具
- 快捷键绑定：为任意工具设置全局热键，一键启动
- 个性化设置：主题切换、背景图、退出行为、Python/Java 路径
- 托盘管理与单实例保护：避免重复启动，支持最小化到托盘
- 便捷操作：右键打开程序目录、在此处启动 CMD/PowerShell

## 目录结构

- 根目录
  - `main.py`：主界面入口（PyQt6）  
  - `loader.py`：启动动画与预加载器，结束后调用主界面  
  - `config.py`：主题、分类、类型常量，工具与设置的读写  
  - `utils.py`：运行环境检测、工具启动、模糊搜索、单实例  
  - `requirements.txt`：开发依赖（PyQt6）
  - `BenD渗透测试工具箱.vbs` / `双击启动工具箱.vbs`：双击启动入口（调用内置 Python）
- 配置与资源
  - `config/settings.json`：应用设置（主题/退出行为/路径等）
  - `config/tools.json`：工具清单（名称/分类/类型/路径/参数/权重等）
  - `config/shortcuts.ini`：工具快捷键映射
  - `config/BenD.ico`：应用图标
- 工具分组
  - `gui_scan/`、`gui_other/`、`gui_shouji/`、`gui_webshell/`：各类工具及其资源
- 内置 Python 运行时
  - `python3/`：嵌入式 Windows Python 3.12 运行时（免安装）

## 快速开始

### 启动应用

- 推荐：在 Windows 上直接双击 `BenD渗透测试工具箱.vbs` 或 `双击启动工具箱.vbs`
- 或者：命令行进入项目根目录执行
  - `python3\python.exe loader.py`
  - 如需跳过动画：`python3\python.exe main.py`

### 添加工具

1. 点击主界面右上角“添加工具”
2. 填写字段：
   - 工具类型：GUI应用 / 命令行 / Python / 批处理 / PowerShell / JAVA8(图形化) / JAVA11(图形化) / JAVA8 / JAVA11 / 网页
   - 路径或网址、启动参数（可选）、分类、权重（0–10）、描述（可选）
3. 保存后自动写入 `config/tools.json`

提示：保存时会将位于项目目录内的绝对路径转换为形如 `/<相对路径>` 的相对写法，提升可移植性。

### 运行工具

- 点击卡片上的“运行”按钮
- 或在卡片菜单中选择“在此处打开 CMD/PowerShell”进行手动执行
- 可在“添加/编辑工具”对话框设置快捷键，之后全局一键触发

## 设置与个性化

- 打开“设置”对话框可配置：
  - 退出模式：每次询问 / 最小化到托盘 / 直接退出
  - 主题：深色 / 浅色 / 护眼 / 粉色 / 蓝色 / 赛博朋克
  - 背景图片：为主界面内容区设置背景图
  - Python 路径：可指定系统 Python 替代内置运行时
  - Java 8/11 路径：为 Java 类工具设置 `java.exe/javaw.exe` 所在目录
- 设置保存至 `config/settings.json`，部分主题变更可能需要重启应用以完全生效（界面会提示是否重启）

## 环境要求

- 操作系统：Windows 10/11（x64）
- 图形界面依赖：PyQt6（开发环境需安装；发布包已内置 Python 运行时）
- 对于 Java 类工具：
  - Java 8：需在设置中配置 `java.exe` 与 `javaw.exe` 所在目录
  - Java 11：同上
  - 若路径无效，应用会给出提示并限制相关工具的运行

## 日志与故障排查

- 运行日志：`app.log`
- 常见问题：
  - 启动无响应：确保未重复实例（应用内有单实例保护）
  - 工具无法运行：检查类型选择是否正确、路径/参数是否有效
  - Java 类工具报错：在“设置”中修正 Java 8/11 的 `bin` 目录
  - Python 工具异常：可配置自定义 Python 解释器（优先级高于系统 Python）

## 架构与代码位置

- 入口与界面
  - 主窗口与 UI 逻辑：[main.py](file:///d:/CTFTools/BenD渗透测试工具箱/main.py)
  - 界面组件（标题栏/搜索/分类/工具网格/设置/添加工具）：[widgets.py](file:///d:/CTFTools/BenD渗透测试工具箱/widgets.py)
  - 启动动画与预加载（读取工具数据）：[loader.py](file:///d:/CTFTools/BenD渗透测试工具箱/loader.py)
- 配置与运行
  - 主题/样式、分类/类型常量、工具与设置读写：[config.py](file:///d:/CTFTools/BenD渗透测试工具箱/config.py)
  - 环境检测、工具启动、搜索与单实例控制：[utils.py](file:///d:/CTFTools/BenD渗透测试工具箱/utils.py)
  - 工具清单与应用设置：  
    - [tools.json](file:///d:/CTFTools/BenD渗透测试工具箱/config/tools.json)  
    - [settings.json](file:///d:/CTFTools/BenD渗透测试工具箱/config/settings.json)

## 开发与运行（可选）

开发者可在系统 Python 环境中运行并调试：

```bash
pip install -r requirements.txt
python main.py
```

如需使用启动动画：

```bash
python loader.py
```

说明：发布目录中已内置 `python3/` 运行时与脚本化启动方式（VBS），无需另外安装 Python。

## 安全与合规

- 本项目为工具聚合与启动器，请在合法合规范围内使用。
- 使用任何第三方工具前，请遵循其各自的许可证与法律法规。

## 致谢

- 社区优秀安全工具及开源项目
- 提供图形界面能力的 PyQt 社区

