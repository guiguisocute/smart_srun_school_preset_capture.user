# Smart SRun School Preset Capture

一个 Tampermonkey（油猴）用户脚本，用来**采集一次真实的深澜 SRun 校园网网页登录**，并自动生成可直接提交给 [smart-srun](https://github.com/matthewlu070111/smart-srun) 的 `school-presets.json` 预设条目。

适用于：浏览器网页登录可用，但你不确定认证地址、`AC_ID`、运营商后缀或高级登录参数，想帮自己学校做一份一键预设的场景。

## 安装

1. 浏览器装好 [Tampermonkey](https://www.tampermonkey.net/)。
2. 点击安装脚本：
   [smart_srun_school_preset_capture.user.js](https://raw.githubusercontent.com/guiguisocute/smart_srun_school_preset_capture.user/main/smart_srun_school_preset_capture.user.js)
   （Tampermonkey 会弹出安装确认页）

## 使用

1. 连上校园网，打开学校的 SRun 认证页（portal）。
2. 在网页登录框里正常输入账号、密码并登录。
3. 页面右侧会出现采集面板，自动显示这次登录抓到的字段：学工号、运营商后缀、认证地址、`AC_ID`、登录形态等。
4. 登录成功后点击「提交信息，协助开发者」，补全脚本无法自动探测的字段：
   - **接入方式**：无线 / 有线（WAN）
   - **SSID**：无线填校园网 SSID，有线可留空
   - **贡献者**：你的 GitHub 用户名（多个用逗号或空格分隔）
   - **学校 ID / 学校名称 / 描述**
5. 点「复制 JSON」或「下载 JSON」，把生成的预设条目粘贴到 smart-srun 的 PR 或 Issue。

> 不熟悉 GitHub PR 流程也没关系，直接开一个 Issue 贴上 JSON 即可。

## 一次抓全所有运营商（抓一个补一个）

运营商后缀在登录请求里就能抓到，**即使这次登录失败也会被记录**。所以你可以用不同运营商的账号多登录几次，脚本会按「抓一个补一个」把抓到的运营商后缀逐个累积进 `operators`，导出的预设更完整。面板会显示「已抓取哪些运营商后缀」。

脚本**不会**预设某学校一定有移动/电信/联通三大运营商，只导出真正抓到过的；运营商后缀统一写在 `operators[].suffix`（空字符串表示纯校园网账号）。

## 隐私

脚本只记录真实请求里出现的字段，**不会导出明文账号、密码、challenge 或加密 `info` 原文**；用户名只保留后缀和打码后的形式。

## 相关项目

- 主项目：[smart-srun](https://github.com/matthewlu070111/smart-srun) —— OpenWrt 上的深澜/SRun 校园网自动认证 LuCI 插件。

## 许可

跟随 smart-srun 主项目的许可协议。
