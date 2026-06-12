# huawei-talent-helper
华为人才在线网课助手，支持自动连播、倍速调节、跳过"本章课件" 和 "随堂测验"。
# 华为人才在线课程助手 (Huawei Talent Helper)

[![License](https://img.shields.io/github/license/你的用户名/huawei-talent-helper)](LICENSE)
[![UserScript](https://img.shields.io/badge/tag-UserScript-orange.svg)](https://www.tampermonkey.net/)
[![Version](https://img.shields.io/badge/version-2.1-blue.svg)]()

一个基于油猴（Tampermonkey）的超轻量级华为人才在线平台网课助手。支持自动连播、倍速调节、跳过"本章课件" 和 "随堂测验"。

## 核心特性

- **强渡盲区（v2.1 特性）**：自动识别「本章课件」、「随堂测验」、「考试作业」等非视频盲区节点。
  - *前置拦截*：在扫描目录树时自动跃迁避让，不误触非视频节点。
  - *黑洞逃逸*：若意外误入无视频页面，子框架将秒级触发逃逸状态，强行激活倒计时弹飞至下一节。
- **层级穿透**：完美攻克多层 `iframe` 隔离，通过底层微任务定时器与 `postMessage` 实现跨域/同域状态融合与指令下发。
- **智能连播**：视频播放结束后自动随机延迟（2s ~ 4s）并平滑切到下一课时，贴合人类行为模式。
- **防挂机拦截**：自动捕获并秒级清理平台弹出的「确定」、「继续观看」等防挂机暂停弹窗。
- **极简控制台**：原生前端注入 UI 面板，支持实时进度查看、随心调节倍速（0.5x - 4.0x）以及自由开关自动连播。

## 🛠️ 安装运行

### 前置准备
1. 确保浏览器已安装 [Tampermonkey (油猴)](https://www.tampermonkey.net/) 浏览器扩展。

### 安装脚本
你可以选择以下任意一种方式安装：
- **方式 A（推荐，支持跟随主分支自动更新）**：
  点击安装链接：[点击直接安装 (Raw Link)](https://raw.githubusercontent.com/Jhaplin/huawei-talent-helper/main/src/huawei-talent-helper.user.js) *(请将链接替换为你自己的实际地址)*
- **方式 B**：复制本仓库 `src/huawei-talent-helper.user.js` 中的完整代码，粘贴至 Tampermonkey 的“添加新脚本”编辑器中保存即可。

## 架构设计简述

项目摒弃了传统的单页面全量扫描方案，采用面向状态的**分布式对等架构**：
1. **顶层窗口（Top Window）**：作为中央大脑，负责渲染美观的宿主 UI 交互面板、管理全局配置（倍速、连播开关）以及统筹全局的跳转倒计时状态机。
2. **子框架环境（Iframe Engine）**：作为高频执行引擎，负责监控原生 `<video>` 状态。当发现激活节点属于黑名单盲区时，伪装成 `ended` 状态向中央大脑汇报，实现无感逃逸。

## 免责声明

1. 本项目仅供网络技术和自动化脚本编写的学习交流使用，切勿用于商业用途或不正当途径。
2. 读者利用本项目的代码或思路所带来的任何直接或间接后果，由使用者自行承担，作者不承担任何法律及连带责任。

## 开源协议

本项目基于 [MIT License](LICENSE) 开源。
