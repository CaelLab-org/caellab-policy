---
title: CaelLabID 开发者守则
description: CaelLabID 开发者守则，约定开发者在接入和使用开放平台时应遵循的行为规范与最佳实践。
sidebar_label: 开发者守则
sidebar_position: 4
---

本守则说明开发者接入 CaelLabID 时应遵守的事项。违反本守则可能影响你的应用访问权限。

---

### 应用注册与管理

- 注册应用时如实填写名称、描述与图标，不冒充其他应用或误导用户；
- 选择与应用功能相符的 `scope`，只申请真正需要的权限；
- 应用不再使用时，建议在[仪表盘](https://id.caellab.com/dashboard)中禁用或删除，避免留下不必要的授权记录。

---

### 客户端凭证安全

- `client_secret` 是应用的身份凭证，不要提交到公开仓库或写在前端代码中；
- 如 `client_secret` 可能已泄露，请立即在仪表盘中重置；
- 建议在服务端完成 Token 交换，不在客户端直接暴露 `client_secret`。

---

### OAuth 流程规范

**授权请求**

- 始终传递 `state` 参数，用于防止 CSRF 攻击；
- `redirect_uri` 必须与注册时填写的回调地址完全一致，包括协议、域名与路径；
- 不要在 `redirect_uri` 中使用通配符或动态拼接。

**Token 使用**

- Access Token 有效期 1 小时，Refresh Token 有效期 180 天，请及时刷新；
- 不要在前端代码中存储 Token，建议在服务端管理；
- 调用 `/api/userinfo` 等接口时，通过 `Authorization: Bearer` 请求头传递 Token；
- 需要撤销 Token 时，调用 `/oauth/revoke`。

**Refresh Token 轮换**

每次使用 Refresh Token 刷新时，旧的 Refresh Token 会失效。请及时保存新的 Refresh Token。

---

### 用户信息保护

- 获取到的用户信息（`sub`、`username`、`email` 等）仅用于你声明的用途；
- 不得将用户信息用于与授权目的无关的用途；
- 不得出售、出租或转让用户信息给第三方；
- 不同应用之间的用户标识（`subject_id`）相互独立，不得通过技术手段关联同一用户在不同应用中的身份。

---

### 内容与行为规范

发布在 CaelLabID 开放平台上的应用与内容：

- 不得违反所在地区法律法规；
- 不得含有恶意代码、病毒、间谍软件等危害用户安全的内容；
- 不得利用 CaelLabID 的登录功能从事钓鱼、欺诈等恶意活动；
- 不得滥用 API 频率限制，或对平台发起自动化攻击与大规模请求。

---

### 频率限制

| 端点 | 限制 |
|------|------|
| `/oauth/token` | 30 次/分钟（IP） |
| `/api/userinfo` | 60 次/分钟（IP） |
| `/api/token-info` | 30 次/分钟（IP） |

超限返回 HTTP 429，响应头包含 `Retry-After` 字段。请在你的应用中做好限流处理。

---

### 交流与反馈

- 接入过程中遇到问题，可在 [XMUER 论坛](https://forum.xmuer.online/) 交流；
- 发现平台 Bug 或有改进建议，请通过邮件告知我们。

---

### 违约处理

如开发行为违反本守则或[服务协议](/id/terms)，我们可能：

- 先通过邮件提醒；
- 情况严重或多次提醒未改善时，暂时限制应用的访问权限；
- 极端情况下终止账号。

---

### 联系方式

📧 [id@caellab.com](mailto:id@caellab.com)

---

虚舟实验室 CaelLabID
**2026 年 10 月 26 日（UTC）**
