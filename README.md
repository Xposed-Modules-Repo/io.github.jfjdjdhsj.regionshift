# 地区伪装 · RegionShift

> **一个模块，同时改掉 Instagram、X、TikTok 看到的国家、语言和时区。**
> 只作用于目标应用进程 —— 不动系统设置、不改安装包签名、不联网、不收集数据。

![LSPosed](https://img.shields.io/badge/LSPosed-API%20102-4F46E5?style=flat-square)
![Android](https://img.shields.io/badge/Android-10%20~%2017-3DDC84?style=flat-square)
![License](https://img.shields.io/badge/License-Non--Commercial-orange?style=flat-square)

<p align="center">
  <img src="https://raw.githubusercontent.com/jfjdjdhsj/RegionShift/main/docs/screenshots/01-main.jpg" width="31%" alt="主界面：三个目标卡片与当前预设" />
  <img src="https://raw.githubusercontent.com/jfjdjdhsj/RegionShift/main/docs/screenshots/02-settings.jpg" width="31%" alt="TikTok 更多设置：SIM / 位置 / 评论翻译" />
  <img src="https://raw.githubusercontent.com/jfjdjdhsj/RegionShift/main/docs/screenshots/03-about.jpg" width="31%" alt="关于与适配：框架状态与已验证版本" />
</p>

---

## 为什么用它

- **一个模块管三个 App** —— 不用为每个应用装一套伪装工具，也不用反复切换
- **切换只要两步** —— 点「更换预设」→ 选地区，语言、时区、运营商一起跟着变
- **真的不动系统** —— 系统语言、系统时区、SIM 状态保持原样，只改目标进程里看到的值
- **随时能还原** —— 关掉开关、重启目标 App，就是原来的环境
- **预设够用也够细** —— 39 个内置地区开箱即用；也能自己拼语言 + 地区 + 时区 + 时间偏移
- **界面不是设置表单** —— 双应用卡片、底部抽屉、可搜索列表、按目标分页的专属设置

## 支持的目标

| 应用 | 已验证版本 | 包名 |
|---|---|---|
| Instagram | 454.0.0.54.77 | `com.instagram.android` |
| X | 12.40.1-prod.01 | `com.twitter.android` |
| TikTok | 47.6.3 | `com.zhiliaoapp.musically` |

- 系统：Android 10 ~ 17（minSdk 29 / targetSdk 37）
- 框架：支持 **libxposed API 102** 的 LSPosed（2.0.3+）
- 通用 Hook 只依赖 Android 框架方法，同版本的其它分包通常仍然有效

## 三步开始

1. **安装** APK，在 LSPosed 里启用「地区伪装」
2. **勾选作用域**：`com.instagram.android`、`com.twitter.android`、`com.zhiliaoapp.musically`（按需勾选）
3. **选预设**：打开模块 App，给每个目标挑一个地区，然后强制停止并重新打开目标 App

> 作用域没勾选的目标会像未安装一样整卡置灰，模块不会注入它的进程。

## 它能改什么

| 维度 | Instagram | X | TikTok |
|---|:---:|:---:|:---:|
| 语言 / 界面文案 | ✅ | ✅ | ✅ |
| 国家 / 地区码 | ✅ | ✅ | ✅ |
| 时区（含 ICU 格式化） | ✅ | ✅ | ✅ |
| 时间偏移（可选） | ✅ | ✅ | ✅ |
| SIM 伪装（运营商 / MCC-MNC / IMSI） | ✅ | — | ✅ |
| 位置伪装（经纬度 / 最后定位） | ✅ | — | ✅ |
| 评论区自动翻译为中文 | — | — | ✅ |

## 使用

- **主界面**：每个目标一张卡片，显示当前预设、语言、时区与生效状态；开关控制该目标是否启用。
- **更换预设**：点卡片上的「更换预设」，底部抽屉里内置与自定义分组展示，当前项打勾。
- **新建 / 编辑**：选国家后语言和时区自动带入，仍可单独改；内置预设只能「另存为副本」。
- **更多设置**（Instagram / TikTok）：SIM 伪装、位置伪装、评论区自动翻译；SIM 地区可「跟随预设」或「自定义」。
- **生效状态**：卡片底部会显示「已应用 / 需重启 / 已关闭 / 未勾选」，点「需重启」可以直接结束并重新拉起目标 App。

## 常见问题

**会不会导致封号？**
模块只改客户端可见的语言、地区、时区等值，不修改登录、不伪造账号归属。风险与任何模块类工具相同，请自行评估。

**切换后为什么没变化？**
语言、地区、时区在多数接口上立即生效，但资源文案和本地缓存需要**强制停止目标 App 再打开**。卡片上的「需重启」可以一键完成。

**为什么卡片是灰色的？**
要么没安装该 App，要么 LSPosed 里没勾选它的作用域。两种情况的处理方式一样：装好 / 勾上，再回到模块 App。

**需要 root 吗？**
只需要 LSPosed。只有「强制停止并重启」会尝试 `su`，失败时会退回系统 API 并提示你手动打开。

**支持哪些版本？**
表格里的版本经过实测。通用 Hook 对同版本其它分包通常有效；TikTok 的专属功能绑定了该版本的少量内部类，升级后可能需要适配。

**改的是系统还是单个 App？**
只改目标 App 进程内看到的值。系统设置、其它 App、账号的服务端归属都不受影响。

## 已知限制

- 只改客户端可见值，不改变账号注册地或服务端判定。
- IP 地址、基站、WiFi 属于网络环境指纹，模块不处理；需要彻底伪装时，网络出口应与所选地区一致。
- App 若在启动早期把语言/地区写入自有缓存或服务端会话，重启后仍可能显示旧值；清除应用数据再登录可消除缓存。
- 时间偏移会同时影响令牌与缓存过期，非必要不要开启；只改时区不需要偏移。

## 隐私

- 不申请网络权限，不收集、不上传任何数据。
- 配置只写入 LSPosed 的 Remote Preferences，必要时在本机暂存。
- 「更多设置」里的 SIM 档案（MCC/MNC、运营商、经纬度）是内置的公开数据，不会向外请求。

## 协议

**允许二次开发，禁止商业使用。** 详见 [LICENSE](https://github.com/jfjdjdhsj/RegionShift/blob/main/LICENSE)。

- 可以：免费使用、修改、二次开发、以相同协议分发
- 不可以：出售、付费分发、内置广告、捆绑销售、作为付费服务的一部分

## 更多

- Hook 点与逆向验证记录：[HOOK.md](https://github.com/jfjdjdhsj/RegionShift/blob/main/HOOK.md)
- 版本更新日志：[CHANGELOG.md](https://github.com/jfjdjdhsj/RegionShift/blob/main/CHANGELOG.md)