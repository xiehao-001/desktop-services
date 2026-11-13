# 桌面系统服务（@eduwork/desktop-services）

> 向 DSH 暴露目录选择、窗口注意力和工作区访问授权三项桌面能力。
>
> Exposes directory picking, window attention requests and workspace access grants to DSH.

## 功能

依赖桌面壳的受认证桥接服务；在纯 Web 部署下不可用。适合需要“让用户选一个本机文件夹”“任务完成时提醒窗口”“申请工作区外的读写授权”的场景。

## 安装

```bash
# 在 DSH 中把本目录作为本地 bundle 安装（绝对路径）
```

安装后由 DSH 插件系统加载，条目 id 为 `desktop-services`。

## 依赖

- `@deepseek-ai/cordis`
- `@deepseek-ai/schemastery`
- `@deepseek-ai/dsh-settings`
- `@deepseek-ai/dsh-session`
- `@deepseek-ai/dsh-host-directory-picker`

## 兼容性

- `engines.dsh`: `>=0.2.1 <0.3.0`
- 与 EduWork 发行版同源，来源于 ECNU/EduWork 仓库。

## 许可

MulanPSL-2.0 AND MIT（与上游 EduWork 一致）。

## 入口修正


- 移除悬空声明：files: docs/**/*（目录不存在）
