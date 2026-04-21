# ☁️ ClawCloud Auto-Login

本项目旨在实现 **每 10 天自动登录一次 ClawCloud (爪云)** 以保持账号活跃。

为了确保自动化脚本顺利运行，**必须**满足以下两个前置条件：
1. ❌ **关闭 Passkey (通行密钥)**：避免脚本无法处理生物识别弹窗。
2. ✅ **开启 2FA (双重验证)**：配合脚本中的 PyOTP 自动生成验证码，绕过异地登录风控。

---

## 🛠️ 配置步骤

### 第一步：Fork 本项目
点击页面右上角的 **Fork** 按钮，将此仓库复制到您的 GitHub 账号下。

### 第二步：开启 GitHub 2FA 并获取密钥
脚本需要通过 2FA 密钥自动计算验证码，因此不能只扫二维码，必须获取**文本密钥**。

1. 登录 GitHub，点击右上角头像 -> **Settings**。
2. 在左侧菜单选择 **Password and authentication**。
3. 找到 "Two-factor authentication" 区域，点击 **Enable 2FA**。
4. 选择 **Set up using an app**。
5. **⚠️ 关键步骤**：
   > 页面显示二维码时，**不要直接点击 Continue**。请点击二维码下方的蓝色小字 **"Setup Key"**（或 "enter this text code"）。
6. **复制显示的字符串密钥**（通常是 16 位字母数字组合）。
   * *注意：同时也请用手机验证器 App (如 Google Auth) 扫描二维码或输入密钥，以完成 GitHub 的验证流程。*

7. **⚠️ 记得把Preferred 2FA method选为Authenticator App，否则脚本不生效**
### 第三步：配置 GitHub Secrets
为了保护您的账号安全，请将敏感信息存储在仓库的 Secrets 中。

1. 进入您的 GitHub 仓库页面。
2. 依次点击导航栏的 **Settings** -> 左侧栏 **Secrets and variables** -> **Actions**。
3. 点击右上角的 **New repository secret** 按钮。
4. 依次添加以下 5 个 Secret：

| Secret 名称 | 填入内容 (Value) | 说明 |
| :--- | :--- | :--- |
| `GH_USERNAME` | **您的 GitHub 账号** | 必填 |
| `GH_PASSWORD` | **您的 GitHub 密码** | 必填 |
| `GH_2FA_SECRET` | **2FA 密钥** | 必填 |
| `TG_BOT_TOKEN` | **你的机器人 Token** | 选填 |
| `TG_CHAT_ID` | **你的个人 ID** | 选填 |

### 第四步：启用工作流权限 (⚠️ 重要)
由于是 Fork 的仓库，GitHub 默认可能会禁用 Actions 以防止滥用。

1. 点击仓库顶部的 **Actions** 选项卡。
2. 如果看到警告提示，请点击绿色的 **"I understand my workflows, go ahead and enable them"** 按钮。

### 第五步：手动测试运行
配置完成后，建议手动触发一次以确保一切正常。

1. 点击 **Actions** 选项卡。
2. 在左侧列表中选择 ** ClawCloud 自动登录（2FA认证）**。
3. 点击右侧的 **Run workflow** 下拉菜单 -> 点击绿色 **Run workflow** 按钮。
4. 等待运行完成，查看日志确保显示 `🎉 登录成功`。
5. TG通知收到截图如下：

   <img width="276" height="84" alt="image" src="https://github.com/user-attachments/assets/18da12e1-a2e8-4dab-8e6f-d0b25f109add" />


**✅ 完成！之后脚本将每隔 10 天自动执行一次保活任务，也可以根据自己需求修改登录天数。**

---

## 🌟 特别鸣谢

本项目基于原作者：[kystor](https://github.com/kystor)、优化作者：[550530](https://github.com/550530)，本人做了些调整，感谢相关作者的贡献。
