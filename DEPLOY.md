# 法务页部署说明(GitHub Pages)

本目录包含 4 个静态页面(index / agreement 用户协议 / privacy 隐私政策 / support 技术支持)+ 样式表,零依赖,可直接托管。

## 部署步骤

1. 在 GitHub 新建一个公开仓库,例如 `neosono-pages`(建议用与开发者账号无关联痕迹的新 GitHub 账号)。
2. 把本目录(`website/`)下的所有文件推到仓库根目录:
   ```bash
   cd website
   git init && git add -A && git commit -m "pages"
   git branch -M main
   git remote add origin git@github.com:<你的账号>/neosono-pages.git
   git push -u origin main
   ```
3. 仓库 Settings → Pages → Source 选 `Deploy from a branch`,Branch 选 `main` / `(root)`,保存。
4. 约 1 分钟后生效,最终地址形如:
   - 用户协议:`https://<你的账号>.github.io/neosono-pages/agreement.html`
   - 隐私政策:`https://<你的账号>.github.io/neosono-pages/privacy.html`
   - 技术支持:`https://<你的账号>.github.io/neosono-pages/support.html`

## 部署后必做

1. 把上面三个最终 URL 替换到 App 源码
   `NeosonoFrame/Features/Account/NSOSignInGateController.swift` 底部的 `NSOLegalDock` 三个常量。
2. App Store Connect 提审信息里:
   - 「技术支持网址」填 support 页 URL;
   - 「隐私政策网址」填 privacy 页 URL。
3. 页面中的联系邮箱 `neosono.support@163.com` 为占位,请改成实际可收发的邮箱(建议新注册一个,与其他产品线隔离)。

## 注意

- 隐私政策中的 SDK 清单(极光推送 / 腾讯云 COS / 腾讯云播放器)与 App 实际集成保持一致;若后续增删 SDK,记得同步更新页面。
- 服务端下发的协议 URL(`/api/website/info` 的 protocols 节点)优先级高于本地兜底 URL;若后台配置了这套新页面地址,App 内展示的就是新页面。
